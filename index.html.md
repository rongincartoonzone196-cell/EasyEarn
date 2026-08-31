<!DOCTYPE html>  
<html lang="bn">  
<head>  
    <meta charset="UTF-8">  
    <meta name="viewport" content="width=device-width, initial-scale=1.0">  
    <title>EasyEarn Ultra-Secure & Premium Platform Pro</title>  
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">  
    <link href="https://fonts.googleapis.com/css2?family=Hind+Siliguri:wght@400;500;600;700&display=swap" rel="stylesheet">  
    <script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>  
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>  
      
    <style>  
        :root {  
            --bg-color: #050811;  
            --app-bg: #f8fafc;  
            --card-bg: #ffffff;  
            --text-dark: #0f172a;  
            --text-muted: #64748b;  
            --primary-purple: #6366f1;  
            --primary-dark: #4f46e5;  
            --accent-glow: rgba(99, 102, 241, 0.5);  
            --bikash-pink: #E2136E;  
            --nagad-orange: #EC1C24;  
            --bank-blue: #2563eb;  
            --green: #10b981;  
            --red: #ef4444;  
            --border-color: #e2e8f0;  
            --transition-smooth: all 0.4s cubic-bezier(0.16, 1, 0.3, 1);  
        }  
  
        * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Hind Siliguri', sans-serif; -webkit-tap-highlight-color: transparent; }  
        body { background-color: var(--bg-color); display: flex; justify-content: center; align-items: center; min-height: 100vh; overflow: hidden; }  
  
        .app-container {  
            width: 100%; max-width: 420px; height: 100vh; max-height: 880px;  
            background-color: var(--app-bg); border-radius: 36px; overflow: hidden;  
            position: relative; box-shadow: 0 35px 70px rgba(0,0,0,0.8), inset 0 1px 0 rgba(255,255,255,0.3);   
            display: flex; flex-direction: column; border: 1.5px solid rgba(255,255,255,0.15);  
        }  
  
        .toast {  
            position: absolute; top: 24px; left: 50%; transform: translateX(-50%) translateY(-20px);  
            background: linear-gradient(135deg, #10b981, #059669); color: white; padding: 13px 24px; border-radius: 28px;  
            font-size: 13.5px; font-weight: 600; opacity: 0; pointer-events: none; transition: var(--transition-smooth); z-index: 3000;   
            box-shadow: 0 12px 30px rgba(16, 185, 129, 0.45); width: 90%; text-align: center; backdrop-filter: blur(10px);   
            border: 1px solid rgba(255,255,255,0.25);  
        }  
        .toast.show { opacity: 1; transform: translateX(-50%) translateY(0); }  
  
        /* AUTH SCREEN */  
        #auth-screen {   
            padding: 28px 22px; display: flex; flex-direction: column; justify-content: flex-start;   
            height: 100%; background: linear-gradient(180deg, #f8fafc 0%, #ede9fe 100%); overflow-y: auto;   
            transition: var(--transition-smooth);  
        }  
        .auth-header { text-align: center; margin-bottom: 22px; }  
        .auth-logo-circle {  
            width: 90px; height: 90px; background: #ffffff;  
            border-radius: 28px; display: flex; align-items: center; justify-content: center;  
            margin: 0 auto 14px auto; box-shadow: 0 15px 30px rgba(99, 102, 241, 0.3);  
            border: 1.5px solid rgba(99, 102, 241, 0.25); transform: scale(1); transition: var(--transition-smooth);  
        }  
        .auth-logo-circle:hover { transform: scale(1.05) rotate(3deg); }  
        .auth-logo-circle i { font-size: 40px; color: var(--primary-purple); }  
        .auth-header h2 { font-size: 32px; font-weight: 800; color: var(--text-dark); letter-spacing: -0.5px; }  
  
        .input-group { margin-bottom: 14px; text-align: left; position: relative; }  
        .input-group label { display: block; font-size: 12.5px; color: var(--text-dark); margin-bottom: 5px; font-weight: 700; }  
          
        .input-with-icon { position: relative; display: flex; align-items: center; }  
        .input-with-icon i.field-icon { position: absolute; left: 18px; color: var(--primary-purple); font-size: 16px; transition: var(--transition-smooth); }  
        .input-with-icon input, .input-group select, .input-group textarea {  
            width: 100%; padding: 13px 18px 13px 48px; border: 1.5px solid var(--border-color); border-radius: 16px; outline: none; font-size: 14px; background: #ffffff; transition: var(--transition-smooth);  
            color: var(--text-dark); box-shadow: 0 2px 8px rgba(0,0,0,0.02);  
        }  
        .input-with-icon input:focus, .input-group select:focus, .input-group textarea:focus {   
            border-color: var(--primary-purple); box-shadow: 0 0 0 5px rgba(99, 102, 241, 0.15); background: #ffffff;  
        }  
        .input-with-icon input:focus ~ i.field-icon { transform: scale(1.1); color: var(--primary-dark); }  
          
        .toggle-password { position: absolute; right: 18px; cursor: pointer; color: var(--text-muted); font-size: 16px; transition: var(--transition-smooth); }  
        .toggle-password:hover { color: var(--primary-purple); }  
  
        .auth-extras { display: flex; justify-content: space-between; align-items: center; margin-top: 8px; margin-bottom: 14px; }  
        .remember-box { display: flex; align-items: center; gap: 8px; cursor: pointer; font-size: 12.5px; color: var(--text-dark); font-weight: 600; }  
        .remember-box input[type="checkbox"] { width: 16px; height: 16px; accent-color: var(--primary-purple); cursor: pointer; }  
        .forgot-pass-link a { font-size: 12.5px; color: var(--primary-purple); font-weight: 600; text-decoration: none; cursor: pointer; }  
        .forgot-pass-link a:hover { text-decoration: underline; }  
  
        .auth-switch-box {  
            text-align: center; margin-top: 12px; background: #ffffff; padding: 14px; border-radius: 16px; border: 1.5px solid var(--border-color);  
            box-shadow: 0 6px 15px rgba(0,0,0,0.02);  
        }  
        .auth-switch-box span { font-size: 12.5px; color: var(--text-muted); font-weight: 600; }  
        .auth-switch-box a { font-size: 12.5px; color: var(--primary-purple); font-weight: 700; text-decoration: none; cursor: pointer; }  
  
        .divider { text-align: center; margin: 12px 0; position: relative; }  
        .divider::before { content: ""; position: absolute; left: 0; top: 50%; width: 100%; height: 1px; background: var(--border-color); }  
        .divider span { background: #f2f2f7; padding: 0 12px; font-size: 11.5px; color: var(--text-muted); position: relative; font-weight: 600; }  
  
        .btn-action {   
            width: 100%; padding: 15px;   
            background: linear-gradient(135deg, #3730a3, #4f46e5, #6366f1);   
            color: white; border: none; border-radius: 16px; font-size: 15.5px; font-weight: 700; cursor: pointer;   
            margin-top: 6px; box-shadow: 0 12px 30px rgba(99, 102, 241, 0.4);   
            transition: var(--transition-smooth); display: flex; align-items: center; justify-content: center; gap: 10px;  
        }  
        .btn-action:hover { transform: translateY(-2px); box-shadow: 0 16px 35px rgba(99, 102, 241, 0.5); }  
        .btn-action:active { transform: scale(0.97); }  
  
        /* MAIN APP STYLING */  
        #main-app { display: none; flex-direction: column; height: 100%; position: relative; background: #f8fafc; }  
        .content { padding: 24px 18px 90px 18px; flex: 1; overflow-y: auto; scroll-behavior: smooth; }  
        .page-view { display: none; }  
        .page-view.active { display: block; animation: fadeInView 0.4s cubic-bezier(0.16, 1, 0.3, 1) forwards; }  
  
        @keyframes fadeInView {  
            from { opacity: 0; transform: translateY(12px); }  
            to { opacity: 1; transform: translateY(0); }  
        }  
  
        .balance-card {  
            background: linear-gradient(135deg, #4f46e5 0%, #6366f1 50%, #818cf8 100%);   
            border-radius: 26px; padding: 24px; color: white; display: flex; justify-content: space-between; align-items: center; margin-bottom: 18px;   
            box-shadow: 0 20px 45px -10px rgba(99, 102, 241, 0.5), inset 0 1px 1px rgba(255,255,255,0.4);  
            border: 1px solid rgba(255, 255, 255, 0.25); position: relative; overflow: hidden;  
        }  
        .balance-amount { font-size: 32px; font-weight: 700; text-shadow: 0 2px 6px rgba(0,0,0,0.15); }  
        .withdraw-pill {   
            background: rgba(255, 255, 255, 0.25); padding: 10px 22px; border-radius: 24px; font-size: 13.5px; font-weight: 700;   
            cursor: pointer; backdrop-filter: blur(12px); border: 1px solid rgba(255,255,255,0.35);  
            box-shadow: 0 10px 20px rgba(0,0,0,0.12); transition: var(--transition-smooth);   
        }  
        .withdraw-pill:hover { background: rgba(255, 255, 255, 0.4); transform: scale(1.06); }  
  
        .vault-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 10px; margin-bottom: 22px; }  
        .vault-box {   
            background: white; border: 1px solid var(--border-color); padding: 16px 8px; border-radius: 18px; text-align: center;   
            box-shadow: 0 6px 15px rgba(0,0,0,0.02); transition: var(--transition-smooth);  
        }  
        .vault-box:hover { transform: translateY(-2px); border-color: var(--primary-purple); }  
        .vault-box p { font-size: 11.5px; color: var(--text-muted); font-weight: 600; }  
        .vault-box h5 { font-size: 14.5px; color: var(--primary-purple); font-weight: 700; margin-top: 5px; }  
  
        .grid-container { display: grid; grid-template-columns: 1fr 1fr; gap: 14px; margin-bottom: 22px; }  
        .menu-card {  
            background: var(--card-bg); border-radius: 22px; padding: 22px 14px; text-align: center;  
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.04); display: flex; flex-direction: column; align-items: center; justify-content: center;   
            cursor: pointer; border: 1px solid rgba(226, 232, 240, 0.8); transition: var(--transition-smooth);  
        }  
        .menu-card:hover { transform: translateY(-4px); box-shadow: 0 18px 40px rgba(99, 102, 241, 0.15); border-color: rgba(99, 102, 241, 0.4); }  
        .icon-circle {   
            width: 54px; height: 54px; border-radius: 22px; background: linear-gradient(135deg, #f1f5f9, #e2e8f0);   
            display: flex; justify-content: center; align-items: center; font-size: 22px; margin-bottom: 14px;  
            box-shadow: inset 0 2px 4px rgba(255,255,255,0.8); transition: var(--transition-smooth);  
        }  
        .menu-card:hover .icon-circle { transform: scale(1.1) rotate(5deg); }  
        .menu-card h4 { font-size: 15.5px; font-weight: 700; color: var(--text-dark); margin-bottom: 4px; }  
        .menu-card p { font-size: 11.5px; color: var(--text-muted); font-weight: 500; }  
  
        .task-box {   
            background: white; border-radius: 22px; padding: 24px; margin-top: 14px; text-align: center;   
            box-shadow: 0 12px 30px rgba(0, 0, 0, 0.03); border: 1px solid var(--border-color);   
        }  
        .back-btn { background: none; border: none; font-size: 15.5px; color: var(--text-dark); font-weight: 700; cursor: pointer; margin-bottom: 18px; display: flex; align-items: center; gap: 8px; transition: var(--transition-smooth); }  
        .back-btn:hover { color: var(--primary-purple); transform: translateX(-3px); }  
  
        .social-item {  
            background: white; padding: 18px; border-radius: 18px; display: flex; justify-content: space-between; align-items: center; margin-bottom: 14px;   
            box-shadow: 0 6px 15px rgba(0,0,0,0.02); border: 1px solid var(--border-color); transition: var(--transition-smooth);  
        }  
        .social-item:hover { border-color: var(--primary-purple); transform: translateY(-2px); box-shadow: 0 10px 25px rgba(99,102,241,0.08); }  
        .social-info { display: flex; align-items: center; gap: 16px; }  
        .social-info i { font-size: 26px; }  
  
        .notice-item-card {  
            background: linear-gradient(135deg, #fff1f2, #ffe4e6); border: 1.5px solid #fecdd3; border-radius: 22px; padding: 18px; margin-bottom: 16px;  
            display: flex; align-items: flex-start; gap: 16px; box-shadow: 0 10px 25px rgba(239, 68, 68, 0.08); position: relative; overflow: hidden; text-align: left;  
        }  
        .notice-item-card::before { content: ""; position: absolute; left: 0; top: 0; bottom: 0; width: 6px; background: var(--red); }  
        .notice-icon-box {  
            width: 42px; height: 42px; background: #fee2e2; color: var(--red); border-radius: 14px; display: flex; align-items: center; justify-content: center; font-size: 20px; flex-shrink: 0; box-shadow: inset 0 2px 4px rgba(255,255,255,0.8);  
        }  
        .notice-content h4 { font-size: 15px; font-weight: 700; color: #9f1239; margin-bottom: 8px; display: flex; align-items: center; gap: 8px; }  
        .notice-content p { font-size: 12.5px; color: #881337; font-weight: 500; line-height: 1.7; white-space: pre-line; }  
  
        .profile-card-header {  
            background: linear-gradient(135deg, #4f46e5 0%, #6366f1 50%, #818cf8 100%);  
            color: white; border-radius: 28px; padding: 28px 22px; text-align: center; margin-bottom: 20px;  
            box-shadow: 0 20px 45px -10px rgba(99, 102, 241, 0.5), inset 0 1px 1px rgba(255,255,255,0.4);  
            border: 1px solid rgba(255, 255, 255, 0.3); position: relative; overflow: hidden;  
        }  
        .profile-avatar {   
            width: 78px; height: 78px; border-radius: 50%; background: rgba(255,255,255,0.25);   
            border: 2.5px solid rgba(255,255,255,0.6); display: flex; align-items: center; justify-content: center;   
            font-size: 34px; margin: 0 auto 14px auto; backdrop-filter: blur(12px);  
            box-shadow: 0 12px 25px rgba(0,0,0,0.2); color: #ffffff;  
        }  
        .stats-row { display: flex; justify-content: space-around; margin-top: 20px; border-top: 1px solid rgba(255,255,255,0.3); padding-top: 16px; }  
  
        .profile-menu-item {   
            background: linear-gradient(135deg, #ffffff 0%, #f8fafc 100%);  
            padding: 16px 20px; border-radius: 22px; display: flex; justify-content: space-between; align-items: center;   
            margin-bottom: 16px; font-weight: 600; color: var(--text-dark); cursor: pointer;   
            border: 1px solid rgba(226, 232, 240, 0.9);  
            box-shadow: 0 10px 25px rgba(99, 102, 241, 0.04), inset 0 1px 1px rgba(255, 255, 255, 0.9);   
            transition: var(--transition-smooth); position: relative; overflow: hidden;  
        }  
        .profile-menu-item:hover {   
            border-color: rgba(99, 102, 241, 0.5); transform: translateY(-3px);   
            box-shadow: 0 16px 35px rgba(99, 102, 241, 0.12), inset 0 1px 2px rgba(255, 255, 255, 1);  
        }  
        .profile-menu-content { display: flex; align-items: center; gap: 18px; }  
        .profile-icon-box {  
            width: 48px; height: 48px; border-radius: 16px; display: flex; align-items: center; justify-content: center;  
            font-size: 20px; box-shadow: 0 8px 18px rgba(0,0,0,0.06), inset 0 2px 3px rgba(255,255,255,0.8);  
            border: 1px solid rgba(255,255,255,0.6);  
        }  
        .profile-arrow-box {  
            width: 32px; height: 32px; border-radius: 50%; background: #f1f5f9; display: flex; align-items: center; justify-content: center;  
            color: #64748b; font-size: 12px; transition: var(--transition-smooth);  
        }  
        .profile-menu-item:hover .profile-arrow-box { background: var(--primary-purple); color: white; transform: translateX(4px); }  
  
        /* ULTRA SMOOTH AI CHAT MODAL */  
        #ai-chat-modal {  
            display: none; position: absolute; inset: 0; background: rgba(15, 23, 42, 0.7);  
            z-index: 2500; backdrop-filter: blur(10px); align-items: flex-end; justify-content: center;  
            animation: fadeInModal 0.3s cubic-bezier(0.16, 1, 0.3, 1) forwards;  
        }  
        @keyframes fadeInModal {  
            from { opacity: 0; }  
            to { opacity: 1; }  
        }  
        .ai-chat-container {  
            width: 100%; height: 90%; background: #ffffff; border-top-left-radius: 40px; border-top-right-radius: 40px;  
            display: flex; flex-direction: column; overflow: hidden; box-shadow: 0 -25px 50px rgba(0,0,0,0.4);  
            animation: slideUpModal 0.4s cubic-bezier(0.16, 1, 0.3, 1) forwards;  
        }  
        @keyframes slideUpModal {  
            from { transform: translateY(100%); }  
            to { transform: translateY(0); }  
        }  
        .ai-chat-header {  
            padding: 20px 24px; background: linear-gradient(135deg, #4f46e5, #6366f1); color: white;  
            display: flex; justify-content: space-between; align-items: center; box-shadow: 0 6px 15px rgba(99, 102, 241, 0.25);  
        }  
        .ai-chat-body {  
            flex: 1; padding: 20px; overflow-y: auto; display: flex; flex-direction: column; gap: 16px; background: #f8fafc;  
            scroll-behavior: smooth;  
        }  
        .ai-message {  
            max-width: 82%; padding: 15px 20px; border-radius: 20px; font-size: 14px; line-height: 1.7; word-break: break-word;  
            animation: messagePop 0.3s cubic-bezier(0.16, 1, 0.3, 1) forwards;  
        }  
        @keyframes messagePop {  
            from { opacity: 0; transform: scale(0.9) translateY(10px); }  
            to { opacity: 1; transform: scale(1) translateY(0); }  
        }  
        .ai-message.bot {  
            background: #ffffff; color: var(--text-dark); align-self: flex-start; border: 1px solid var(--border-color);  
            box-shadow: 0 6px 18px rgba(0,0,0,0.03); border-bottom-left-radius: 6px;  
        }  
        .ai-message.user {  
            background: linear-gradient(135deg, #4f46e5, #6366f1); color: white; align-self: flex-end;   
            box-shadow: 0 8px 20px rgba(99, 102, 241, 0.35); border-bottom-right-radius: 6px;  
        }  
        .ai-typing-indicator {  
            display: flex; align-items: center; gap: 6px; padding: 14px 18px; background: #ffffff; border: 1px solid var(--border-color);  
            border-radius: 18px; align-self: flex-start; border-bottom-left-radius: 6px; width: fit-content;  
            box-shadow: 0 4px 12px rgba(0,0,0,0.02);  
        }  
        .ai-typing-dot {  
            width: 8px; height: 8px; background: var(--primary-purple); border-radius: 50%; opacity: 0.4;  
            animation: typingBounce 1.2s infinite ease-in-out;  
        }  
        .ai-typing-dot:nth-child(2) { animation-delay: 0.2s; }  
        .ai-typing-dot:nth-child(3) { animation-delay: 0.4s; }  
        @keyframes typingBounce {  
            0%, 80%, 100% { transform: translateY(0); opacity: 0.4; }  
            40% { transform: translateY(-8px); opacity: 1; }  
        }  
  
        .ai-chat-footer {  
            padding: 16px 20px; background: white; border-top: 1px solid var(--border-color); display: flex; gap: 12px; align-items: center;  
        }  
        .ai-chat-input {  
            flex: 1; padding: 14px 20px; border: 1.5px solid var(--border-color); border-radius: 18px; outline: none; font-size: 14.5px; background: #f8fafc; transition: var(--transition-smooth);  
        }  
        .ai-chat-input:focus { border-color: var(--primary-purple); background: #ffffff; box-shadow: 0 0 0 5px rgba(99, 102, 241, 0.12); }  
        .ai-send-btn {  
            background: var(--primary-purple); color: white; border: none; width: 52px; height: 52px; border-radius: 18px;  
            display: flex; align-items: center; justify-content: center; cursor: pointer; font-size: 18px; transition: var(--transition-smooth);  
            box-shadow: 0 8px 20px rgba(99, 102, 241, 0.35);  
        }  
        .ai-send-btn:hover { background: var(--primary-dark); transform: scale(1.08); }  
  
        .withdraw-card {  
            background: linear-gradient(135deg, #4f46e5 0%, #6366f1 50%, #818cf8 100%);  
            border-radius: 30px; padding: 28px 24px; color: white;  
            box-shadow: 0 28px 55px -12px rgba(99, 102, 241, 0.55), inset 0 1px 1px rgba(255,255,255,0.4);  
            border: 1px solid rgba(255, 255, 255, 0.35); position: relative; overflow: hidden;  
        }  
          
        .method-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 12px; margin: 20px 0 26px 0; }  
        .method-item {  
            background: rgba(255, 255, 255, 0.12); border: 1.5px solid rgba(255, 255, 255, 0.25);  
            border-radius: 18px; padding: 16px 10px; text-align: center; cursor: pointer;  
            transition: var(--transition-smooth); display: flex; flex-direction: column; align-items: center; gap: 10px;  
            backdrop-filter: blur(14px); box-shadow: inset 0 1px 1px rgba(255,255,255,0.25);  
        }  
        .method-item i { font-size: 24px; transition: var(--transition-smooth); }  
        .method-item span { font-size: 13.5px; font-weight: 600; color: #f8fafc; }  
        .method-item:hover { background: rgba(255, 255, 255, 0.25); border-color: rgba(255, 255, 255, 0.5); transform: translateY(-3px); }  
  
        .method-item.active {  
            border-color: #ffffff; background: rgba(255, 255, 255, 0.35);  
            box-shadow: 0 15px 35px -5px rgba(0, 0, 0, 0.25), inset 0 1px 2px rgba(255,255,255,0.5);  
        }  
        .method-item.active span { color: #ffffff; font-weight: 700; }  
        .method-item.active i { color: #ffffff !important; transform: scale(1.2); filter: drop-shadow(0 3px 8px rgba(0,0,0,0.4)); }  
  
        .withdraw-input {  
            background: rgba(255, 255, 255, 0.18) !important; border: 1.5px solid rgba(255, 255, 255, 0.35) !important;  
            color: white !important; border-radius: 16px !important; padding: 14px 18px !important;  
            transition: var(--transition-smooth) !important; backdrop-filter: blur(10px);  
        }  
        .withdraw-input:focus {  
            border-color: #ffffff !important; background: rgba(255, 255, 255, 0.28) !important;  
            box-shadow: 0 0 0 5px rgba(255, 255, 255, 0.25) !important;  
        }  
        .withdraw-input::placeholder { color: rgba(255, 255, 255, 0.7); }  
  
        .btn-withdraw-action {  
            width: 100%; padding: 16px; background: #ffffff; color: var(--primary-purple);  
            border: none; border-radius: 16px; font-size: 16px; font-weight: 700; cursor: pointer;  
            margin-top: 8px; box-shadow: 0 15px 35px rgba(0, 0, 0, 0.3), inset 0 1px 1px rgba(255,255,255,0.9);  
            transition: var(--transition-smooth);  
        }  
        .btn-withdraw-action:hover { transform: translateY(-3px); background: #f8fafc; box-shadow: 0 20px 40px rgba(0, 0, 0, 0.4); }  
  
        .referral-hero-card {  
            background: linear-gradient(135deg, #FF7954 0%, #FFB75E 100%);  
            border-radius: 24px; padding: 24px; color: white; display: flex; align-items: center; margin-bottom: 18px;  
            box-shadow: 0 15px 35px rgba(255, 121, 84, 0.35), inset 0 1px 1px rgba(255,255,255,0.4);  
            border: 1px solid rgba(255,255,255,0.25);  
        }  
        .referral-hero-icon { font-size: 44px; margin-right: 18px; filter: drop-shadow(0 3px 6px rgba(0,0,0,0.2)); }  
        .referral-hero-text h3 { font-size: 16.5px; font-weight: 700; margin-bottom: 3px; }  
        .referral-hero-text p { font-size: 26px; font-weight: bold; text-shadow: 0 2px 6px rgba(0,0,0,0.15); }  
  
        .ref-box-container {  
            background: white; border-radius: 22px; padding: 22px; border: 1px solid var(--border-color); margin-bottom: 22px;  
            box-shadow: 0 10px 25px rgba(0,0,0,0.03);  
        }  
        .ref-input-group {  
            display: flex; background: #f1f5f9; border-radius: 16px; overflow: hidden; border: 1.5px solid var(--border-color); margin-top: 12px;  
        }  
        .ref-input-group input { flex: 1; border: none; background: transparent; padding: 15px; font-size: 13.5px; color: var(--text-dark); outline: none; font-family: monospace; }  
        .ref-copy-btn { background: var(--primary-purple); color: white; border: none; padding: 0 20px; font-weight: 700; cursor: pointer; font-size: 13.5px; transition: var(--transition-smooth); }  
        .ref-copy-btn:hover { background: var(--primary-dark); }  
  
        .leaderboard-list { background: white; border-radius: 22px; overflow: hidden; border: 1px solid var(--border-color); box-shadow: 0 10px 25px rgba(0,0,0,0.03); }  
        .leaderboard-item { display: flex; align-items: center; padding: 16px 20px; border-bottom: 1px solid #f1f5f9; transition: var(--transition-smooth); }  
        .leaderboard-item:last-child { border-bottom: none; }  
        .leaderboard-item:hover { background: #f8fafc; }  
        .rank-badge { width: 36px; height: 36px; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-weight: bold; font-size: 14.5px; margin-right: 16px; box-shadow: 0 6px 12px rgba(0,0,0,0.1); }  
        .rank-1 { background: linear-gradient(135deg, #FFD700, #FFA500); color: #5c3a00; }  
        .rank-2 { background: linear-gradient(135deg, #E0E0E0, #9E9E9E); color: #333333; }  
        .rank-3 { background: linear-gradient(135deg, #E69A55, #A0522D); color: #fff; }  
  
        .bottom-nav {   
            position: absolute; bottom: 0; left: 0; right: 0; background: rgba(255, 255, 255, 0.95);   
            display: flex; justify-content: space-around; padding: 16px 0 20px 0;   
            border-top: 1px solid rgba(226, 232, 240, 0.8); border-bottom-left-radius: 36px; border-bottom-right-radius: 36px;   
            backdrop-filter: blur(14px); box-shadow: 0 -12px 30px rgba(0,0,0,0.06); z-index: 10;  
        }  
        .nav-item { display: flex; flex-direction: column; align-items: center; color: var(--text-muted); font-size: 11.5px; font-weight: 600; cursor: pointer; transition: var(--transition-smooth); }  
        .nav-item i { font-size: 20px; margin-bottom: 5px; transition: var(--transition-smooth); }  
        .nav-item.active { color: var(--primary-purple); }  
        .nav-item.active i { transform: scale(1.2); filter: drop-shadow(0 3px 6px rgba(99,102,241,0.35)); }  
  
        /* LOADING SPINNER OVERLAY */  
        .app-loader {  
            position: absolute; inset: 0; background: rgba(9, 13, 22, 0.85); backdrop-filter: blur(8px);  
            z-index: 4000; display: flex; flex-direction: column; align-items: center; justify-content: center; color: white;  
            opacity: 0; pointer-events: none; transition: opacity 0.3s ease;  
        }  
        .app-loader.active { opacity: 1; pointer-events: auto; }  
        .spinner {  
            width: 50px; height: 50px; border: 4px solid rgba(255,255,255,0.2); border-top-color: var(--primary-purple);  
            border-radius: 50%; animation: spin 0.8s linear infinite; margin-bottom: 14px;  
        }  
        @keyframes spin { to { transform: rotate(360deg); } }  
    </style>  
</head>  
<body>  
  
    <div class="app-container">  
        <div id="toast" class="toast">বার্তা তথ্য</div>  
  
        <!-- GLOBAL LOADER -->  
        <div id="app-loader" class="app-loader">  
            <div class="spinner"></div>  
            <p style="font-weight: 600; font-size: 14px; letter-spacing: 0.5px;">প্রক্রিয়াধীন রয়েছে...</p>  
        </div>  
  
        <!-- ENHANCED AI CHAT MODAL -->  
        <div id="ai-chat-modal">  
            <div class="ai-chat-container">  
                <div class="ai-chat-header">  
                    <div style="display: flex; align-items: center; gap: 12px;">  
                        <i class="fa-solid fa-robot" style="font-size: 22px;"></i>  
                        <h4 style="font-size: 16px; font-weight: 700;">EasyEarn এআই স্মার্ট সাপোর্ট অ্যাসিস্ট্যান্ট</h4>  
                    </div>  
                    <i class="fa-solid fa-xmark" style="font-size: 20px; cursor: pointer; padding: 6px; transition: var(--transition-smooth);" onclick="closeAIChat()"></i>  
                </div>  
                <div class="ai-chat-body" id="ai-chat-messages">  
                    <div class="ai-message bot">হ্যালো! আমি EasyEarn-এর সুপার এআই সহকারী। টাকা উইথড্র, কাজ করা, রেফার বা যেকোনো সিকিউরিটি সংক্রান্ত প্রশ্ন থাকলে আমাকে বলুন, আমি তাৎক্ষণিক সমাধান দেব! 😊</div>  
                </div>  
                <div class="ai-chat-footer">  
                    <input type="text" id="ai-user-input" class="ai-chat-input" placeholder="আপনার প্রশ্ন বা সমস্যা এখানে লিখুন..." onkeypress="handleAIPress(event)">  
                    <button class="ai-send-btn" onclick="sendAIMessage()"><i class="fa-solid fa-paper-plane"></i></button>  
                </div>  
            </div>  
        </div>  
  
        <!-- AUTH SCREEN -->  
        <div id="auth-screen">  
            <div id="signup-container">  
                <div class="auth-header">  
                    <div class="auth-logo-circle"><i class="fa-solid fa-shield-halved"></i></div>  
                    <h2>EasyEarn</h2>  
                    <p style="font-size: 13px; color: var(--text-muted); margin-top: 4px;">আল্ট্রা সিকিউরড প্রিমিয়াম আর্নিং প্ল্যাটফর্ম</p>  
                </div>  
  
                <form id="signup-form" autocomplete="on" onsubmit="handleSignup(event)">  
                    <div class="input-group">  
                        <label>পুরো নাম</label>  
                        <div class="input-with-icon">  
                            <i class="fa-regular fa-user field-icon"></i>  
                            <input type="text" id="reg-name" autocomplete="name" placeholder="আপনার পুরো নাম লিখুন" required>  
                        </div>  
                    </div>  
                    <div class="input-group">  
                        <label>মোবাইল নম্বর</label>  
                        <div class="input-with-icon">  
                            <i class="fa-solid fa-mobile-screen field-icon"></i>  
                            <input type="tel" id="reg-phone" autocomplete="tel" placeholder="017XXXXXXXX" required>  
                        </div>  
                    </div>  
                    <div class="input-group">  
                        <label>ইমেইল এড্রেস</label>  
                        <div class="input-with-icon">  
                            <i class="fa-regular fa-envelope field-icon"></i>  
                            <input type="email" id="reg-email" autocomplete="email" placeholder="example@gmail.com" required>  
                        </div>  
                    </div>  
                    <div class="input-group">  
                        <label>পাসওয়ার্ড</label>  
                        <div class="input-with-icon">  
                            <i class="fa-solid fa-lock field-icon"></i>  
                            <input type="password" id="reg-pass" autocomplete="new-password" placeholder="কমপক্ষে ৬ ডিজিটের পাসওয়ার্ড" required>  
                            <i class="fa-solid fa-eye-slash toggle-password" onclick="togglePass('reg-pass', this)"></i>  
                        </div>  
                    </div>  
                    <div class="input-group">  
                        <label>কনফার্ম পাসওয়ার্ড</label>  
                        <div class="input-with-icon">  
                            <i class="fa-solid fa-lock field-icon"></i>  
                            <input type="password" id="reg-cpass" autocomplete="new-password" placeholder="পুনরায় পাসওয়ার্ড দিন" required>  
                            <i class="fa-solid fa-eye-slash toggle-password" onclick="togglePass('reg-cpass', this)"></i>  
                        </div>  
                    </div>  
                      
                    <button type="submit" class="btn-action">রেজিস্ট্রেশন করুন <i class="fa-solid fa-arrow-right"></i></button>  
                </form>  
  
                <div class="auth-switch-box" style="margin-top: 14px;">  
                    <span>ইতিমধ্যেই অ্যাকাউন্ট আছে? </span>  
                    <a onclick="switchAuthTab('login')">লগইন করুন</a>  
                </div>  
            </div>  
  
            <div id="login-container" style="display: none;">  
                <div class="auth-header">  
                    <div class="auth-logo-circle"><i class="fa-solid fa-shield-halved"></i></div>  
                    <h2>EasyEarn</h2>  
                    <p style="font-size: 13px; color: var(--text-muted); margin-top: 4px;">আপনার অ্যাকাউন্টে নিরাপদে প্রবেশ করুন</p>  
                </div>  
  
                <form id="login-form" autocomplete="on" onsubmit="handleLogin(event)">  
                    <div class="input-group">  
                        <label>মোবাইল নম্বর</label>  
                        <div class="input-with-icon">  
                            <i class="fa-solid fa-mobile-screen field-icon"></i>  
                            <input type="tel" id="login-phone" name="username" autocomplete="username tel" placeholder="017XXXXXXXX" required>  
                        </div>  
                    </div>  
                    <div class="input-group">  
                        <label>পাসওয়ার্ড</label>  
                        <div class="input-with-icon">  
                            <i class="fa-solid fa-lock field-icon"></i>  
                            <input type="password" id="login-pass" name="password" autocomplete="current-password" placeholder="********" required>  
                            <i class="fa-solid fa-eye-slash toggle-password" onclick="togglePass('login-pass', this)"></i>  
                        </div>  
                    </div>  
  
                    <div class="auth-extras">  
                        <label class="remember-box">  
                            <input type="checkbox" id="remember-me"> পাসওয়ার্ড সেভ করুন  
                        </label>  
                        <div class="forgot-pass-link">  
                            <a onclick="showForgotModal()">পাসওয়ার্ড ভুলে গেছেন?</a>  
                        </div>  
                    </div>  
  
                    <button type="submit" class="btn-action">লগইন করুন <i class="fa-solid fa-arrow-right"></i></button>  
                </form>  
  
                <div class="divider"><span>অথবা</span></div>  
  
                <div class="auth-switch-box">  
                    <span>আপনার কি অ্যাকাউন্ট নেই? </span>  
                    <a onclick="switchAuthTab('signup')">রেজিস্ট্রেশন করুন</a>  
                </div>  
            </div>  
        </div>  
  
        <!-- MAIN APP -->  
        <div id="main-app">  
            <input type="hidden" id="sec-csrf-token" value="">  
            <div class="content">  
  
                <!-- হোম পেজ -->  
                <div id="view-home" class="page-view active">  
                    <div class="balance-card">  
                        <div>  
                            <p style="font-size:12.5px; opacity: 0.85; font-weight: 500;">মূল ব্যালেন্স</p>  
                            <div class="balance-amount">৳ <span class="val-balance">0.00</span></div>  
                        </div>  
                        <div class="withdraw-pill" onclick="openPage('withdraw')"><i class="fa-solid fa-arrow-up-right-from-square" style="margin-right: 6px;"></i> উইথড্র</div>  
                    </div>  
  
                    <div class="vault-grid">  
                        <div class="vault-box">  
                            <p>এক্সট্রা ব্যালেন্স</p>  
                            <h5>৳ 0.00</h5>  
                        </div>  
                        <div class="vault-box">  
                            <p>বোনাস ওয়ালেট</p>  
                            <h5>৳ 0.00</h5>  
                        </div>  
                        <div class="vault-box">  
                            <p>পেন্ডিং ক্যাশ</p>  
                            <h5>৳ 0.00</h5>  
                        </div>  
                    </div>  
  
                    <div class="grid-container">  
                        <div class="menu-card" onclick="openPage('video')">  
                            <div class="icon-circle" style="color:#ef4444;"><i class="fa-solid fa-tv"></i></div>  
                            <h4>ভিডিও টাস্ক</h4>  
                            <p>ডেইলি ভিডিও দেখুন</p>  
                        </div>  
                        <div class="menu-card" onclick="openPage('social')">  
                            <div class="icon-circle" style="color:#0284c7;"><i class="fa-solid fa-share-nodes"></i></div>  
                            <h4>সোশ্যাল টাস্ক</h4>  
                            <p>Telegram, TikTok, YT</p>  
                        </div>  
                        <div class="menu-card" onclick="openPage('quiz')">  
                            <div class="icon-circle" style="color:#16a34a;"><i class="fa-solid fa-pen-to-square"></i></div>  
                            <h4>কুইজ ম্যাচ</h4>  
                            <p>উত্তর দিয়ে আয় করুন</p>  
                        </div>  
                        <div class="menu-card" onclick="openPage('survey')">  
                            <div class="icon-circle" style="color:#d97706;"><i class="fa-solid fa-clipboard-list"></i></div>  
                            <h4>সার্ভে কাজ</h4>  
                            <p>মতামত শেয়ার করুন</p>  
                        </div>  
                        <div class="menu-card" onclick="openPage('captcha')">  
                            <div class="icon-circle" style="color:#ea580c;"><i class="fa-solid fa-keyboard"></i></div>  
                            <h4>টাইপিং ও ক্যাপচা</h4>  
                            <p>সহজ ফিলাপ কাজ</p>  
                        </div>  
                        <div class="menu-card" onclick="openPage('refer')">  
                            <div class="icon-circle" style="color:#db2777;"><i class="fa-solid fa-bullhorn"></i></div>  
                            <h4>রেফার ও ইনকাম</h4>  
                            <p>বন্ধুদের আমন্ত্রণ দিন</p>  
                        </div>  
                    </div>  
                </div>  
  
                <!-- কুইজ পেজ -->  
                <div id="view-quiz" class="page-view">  
                    <button class="back-btn" onclick="openPage('home')"><i class="fa-solid fa-arrow-left"></i> ব্যাক</button>  
                    <h3>কুইজ ম্যাচ ও সিকিউর বোনাস</h3>  
                    <div class="task-box">  
                        <p id="quiz-question" style="font-weight:700; font-size:16.5px; margin-bottom:20px; color:var(--text-dark);">প্রশ্ন লোড হচ্ছে...</p>  
                        <div id="quiz-options"></div>  
                    </div>  
                </div>  
  
                <!-- সার্ভে পেজ -->  
                <div id="view-survey" class="page-view">  
                    <button class="back-btn" onclick="openPage('home')"><i class="fa-solid fa-arrow-left"></i> ব্যাক</button>  
                    <h3>ডেইলি সার্ভে প্যানেল</h3>  
                    <div class="task-box" style="text-align: left;">  
                        <p style="font-weight:600; margin-bottom:8px; font-size:13.5px;">১. আপনি প্রতিদিন কত সময় অনলাইনে থাকেন?</p>  
                        <div class="input-group">  
                            <select id="survey-ans">  
                                <option>১ - ২ ঘণ্টা</option>  
                                <option>৩ - ৫ ঘণ্টা</option>  
                                <option>৫ ঘণ্টার বেশি</option>  
                            </select>  
                        </div>  
                        <p style="font-weight:600; margin-bottom:8px; font-size:13.5px;">২. আপনার প্রিয় প্ল্যাটফর্ম কোনটি?</p>  
                        <div class="input-group">  
                            <input type="text" id="survey-input" placeholder="যেমন: YouTube/Facebook">  
                        </div>  
                        <button class="btn-action" onclick="submitSurvey()">সার্ভে জমা দিন (+৳১৫)</button>  
                    </div>  
                </div>  
  
                <!-- সোশ্যাল টাস্ক পেজ -->  
                <div id="view-social" class="page-view">  
                    <button class="back-btn" onclick="openPage('home')"><i class="fa-solid fa-arrow-left"></i> ব্যাক</button>  
                    <h3>সোশ্যাল মিডিয়া টাস্ক</h3>  
                      
                    <div class="social-item">  
                        <div class="social-info">  
                            <i class="fa-brands fa-telegram" style="color:#229ED9;"></i>  
                            <div>  
                                <p style="font-weight:700; font-size:14.5px;">Telegram চ্যানেল</p>  
                                <p style="font-size:11.5px; color:var(--text-muted);">জয়েন করুন (+৳৮)</p>  
                            </div>  
                        </div>  
                        <button class="btn-action" style="width:auto; padding:9px 16px; font-size:12.5px;" onclick="addMoney(8, 'Telegram জয়েন সফল!')">জয়েন</button>  
                    </div>  
  
                    <div class="social-item">  
                        <div class="social-info">  
                            <i class="fa-brands fa-tiktok" style="color:#000000;"></i>  
                            <div>  
                                <p style="font-weight:700; font-size:14.5px;">TikTok অ্যাকাউন্ট</p>  
                                <p style="font-size:11.5px; color:var(--text-muted);">ফলো করুন (+৳৫)</p>  
                            </div>  
                        </div>  
                        <button class="btn-action" style="width:auto; padding:9px 16px; font-size:12.5px;" onclick="addMoney(5, 'TikTok ফলো সফল!')">ফলো</button>  
                    </div>  
  
                    <div class="social-item">  
                        <div class="social-info">  
                            <i class="fa-brands fa-youtube" style="color:#FF0000;"></i>  
                            <div>  
                                <p style="font-weight:700; font-size:14.5px;">YouTube চ্যানেল</p>  
                                <p style="font-size:11.5px; color:var(--text-muted);">সাবস্ক্রাইব করুন (+৳১০)</p>  
                            </div>  
                        </div>  
                        <button class="btn-action" style="width:auto; padding:9px 16px; font-size:12.5px;" onclick="addMoney(10, 'YouTube সাবস্ক্রাইব সফল!')">সাবস্ক্রাইব</button>  
                    </div>  
                </div>  
  
                <!-- রিপোর্ট পেজ -->  
                <div id="view-report" class="page-view">  
                    <h3 style="margin-bottom: 14px;">আয়ের হিসেব ও সিকিউরিটি অডিট</h3>  
                    <div class="task-box" style="margin-bottom: 18px; text-align: left; background: linear-gradient(135deg, #f8fafc, #f1f5f9);">  
                        <p style="color:var(--text-muted); font-size:12.5px; font-weight: 600;">সর্বমোট উপার্জিত অর্থ</p>  
                        <h2 style="color:var(--green); font-size: 28px; margin-top: 6px;">৳ <span class="val-balance">0.00</span></h2>  
                    </div>  
                    <p style="font-weight:700; font-size:14.5px; margin-bottom:12px;">সাম্প্রतिक সিকিউর্ড লেনদেন</p>  
                    <div class="history-list" id="history-list-box">  
                        <div style="font-size:12.5px; color:var(--text-muted); text-align:center; padding:24px; background:white; border-radius:18px; border: 1px solid var(--border-color);">কোনো লেনদেন পাওয়া যায়নি।</div>  
                    </div>  
                </div>  
  
                <!-- জরুরি নোটিফিকেশন পেজ -->  
                <div id="view-emergency" class="page-view">  
                    <button class="back-btn" onclick="openPage('home')"><i class="fa-solid fa-arrow-left"></i> ব্যাক</button>  
                    <h3 style="margin-bottom: 16px;">জরুরি নোটিফিকেশন</h3>  
                      
                    <div class="notice-item-card">  
                        <div class="notice-icon-box"><i class="fa-solid fa-triangle-exclamation"></i></div>  
                        <div class="notice-content">  
                            <h4>জরুরি ঘোষণা ও কঠোর সতর্কবার্তা! 🚨 <span style="font-size: 10px; background: var(--red); color: white; padding: 2px 8px; border-radius: 6px;">Live</span></h4>  
                            <p>সবাইকে অত্যন্ত গুরুত্বের সাথে জানানো যাচ্ছে যে, প্ল্যাটফর্মের নির্দিষ্ট নিয়মকানুনগুলো সবাইকে কঠোরভাবে মেনে চলতে হবে। কোনো অবস্থাতেই কেউ নিয়ম ভঙ্গ করবেন না। ⚠️  
📌 বিশেষ নির্দেশনা:  
ভুয়া বা অসদুপায় অবলম্বন করে কাজ করার চেষ্টা করলে তাৎক্ষণিকভাবে অ্যাকাউন্ট চিরতরে ব্যান করা হবে। ❌  
পেমেন্ট রিকোয়েস্ট দেওয়ার আগে অবশ্যই প্রোফাইল এবং বিকাশ/নগদ নম্বর সঠিকভাবে চেক করে নেবেন। 💳  
অ্যাডমিন বা সাপোর্ট টিমের নাম ভাঙিয়ে কেউ প্রতারণা করার চেষ্টা করলে সাথে সাথে রিপোর্ট করুন। 🛡️</p>  
                        </div>  
                    </div>  
                </div>  
  
                <!-- প্রোফাইল পেজ -->  
                <div id="view-profile" class="page-view">  
                    <div class="profile-card-header">  
                        <div class="profile-avatar"><i class="fa-solid fa-user-shield"></i></div>  
                        <h3 id="display-name" style="font-size: 19px; font-weight: 700; letter-spacing: 0.5px;">ব্যবহারকারী</h3>  
                        <p style="font-size:12.5px; opacity: 0.85; margin-top: 3px;" id="display-phone">017XXXXXXXX</p>  
                        <div class="stats-row">  
                            <div>  
                                <p style="font-size:11.5px; opacity: 0.8;">মোট টাস্ক</p>  
                                <h4 style="font-size: 14.5px; font-weight: 700;">০ টি</h4>  
                            </div>  
                            <div>  
                                <p style="font-size:11.5px; opacity: 0.8;">সিকিউরিটি স্টেট</p>  
                                <h4 style="font-size: 14.5px; font-weight: 700; color: #34d399;">SSL এনক্রিপ্টেড</h4>  
                            </div>  
                        </div>  
                    </div>  
  
                    <div class="profile-menu-item" onclick="openPage('report')">  
                        <div class="profile-menu-content">  
                            <div class="profile-icon-box" style="background: linear-gradient(135deg, #eff6ff, #dbeafe); color: #2563eb;"><i class="fa-solid fa-receipt"></i></div>  
                            <div>  
                                <div style="font-size: 14.5px; font-weight: 700; color: var(--text-dark);">হিস্ট্রি ও রিপোর্ট</div>  
                                <div style="font-size: 11.5px; color: var(--text-muted); font-weight: 500;">লেনদেন ও আয়ের বিবরণী</div>  
                            </div>  
                        </div>  
                        <div class="profile-arrow-box"><i class="fa-solid fa-chevron-right"></i></div>  
                    </div>  
  
                    <div class="profile-menu-item" onclick="openPage('help')">  
                        <div class="profile-menu-content">  
                            <div class="profile-icon-box" style="background: linear-gradient(135deg, #f0fdf4, #dcfce7); color: #16a34a;"><i class="fa-solid fa-headset"></i></div>  
                            <div>  
                                <div style="font-size: 14.5px; font-weight: 700; color: var(--text-dark);">হেল্প সেন্টার ও সাপোর্ট</div>  
                                <div style="font-size: 11.5px; color: var(--text-muted); font-weight: 500;">২৪/৭ লাইভ কাস্টমার কেয়ার</div>  
                            </div>  
                        </div>  
                        <div class="profile-arrow-box"><i class="fa-solid fa-chevron-right"></i></div>  
                    </div>  
  
                    <div class="profile-menu-item" onclick="openAIChat()">  
                        <div class="profile-menu-content">  
                            <div class="profile-icon-box" style="background: linear-gradient(135deg, #faf5ff, #f3e8ff); color: #9333ea;"><i class="fa-solid fa-robot"></i></div>  
                            <div>  
                                <div style="font-size: 14.5px; font-weight: 700; color: var(--text-dark);">এআই সাপোর্ট অ্যাসিস্ট্যান্ট</div>  
                                <div style="font-size: 11.5px; color: var(--text-muted); font-weight: 500;">যেকোনো প্রশ্নের তাৎক্ষণিক উত্তর নিন</div>  
                            </div>  
                        </div>  
                        <div class="profile-arrow-box" style="background: #f3e8ff; color: #9333ea;"><i class="fa-solid fa-chevron-right"></i></div>  
                    </div>  
  
                    <div class="profile-menu-item" onclick="SecurityModule.logout()" style="border-color: rgba(239, 68, 68, 0.25); background: linear-gradient(135deg, #ffffff, #fff1f2);">  
                        <div class="profile-menu-content">  
                            <div class="profile-icon-box" style="background: linear-gradient(135deg, #fef2f2, #fee2e2); color: #ef4444;"><i class="fa-solid fa-right-from-bracket"></i></div>  
                            <div>  
                                <div style="font-size: 14.5px; font-weight: 700; color: #ef4444;">লগআউট করুন</div>  
                                <div style="font-size: 11.5px; color: #f87171; font-weight: 500;">সুরক্ষিতভাবে অ্যাকাউন্ট বন্ধ করুন</div>  
                            </div>  
                        </div>  
                        <div class="profile-arrow-box" style="background: #fee2e2; color: #ef4444;"><i class="fa-solid fa-arrow-right-from-bracket"></i></div>  
                    </div>  
                </div>  
  
                <!-- হেল্প পেজ -->  
                <div id="view-help" class="page-view">  
                    <button class="back-btn" onclick="openPage('profile')"><i class="fa-solid fa-arrow-left"></i> ব্যাক</button>  
                    <h3>হেল্প সেন্টার ও সাপোর্ট</h3>  
                      
                    <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 12px; margin-bottom: 16px;">  
                        <a href="https://t.me/SOHAGHASAN196x" target="_blank" style="text-decoration: none;">  
                            <div style="background: #229ED9; color: white; padding: 16px; border-radius: 18px; text-align: center; box-shadow: 0 6px 15px rgba(34, 158, 217, 0.35); display: flex; flex-direction: column; align-items: center; gap: 8px; transition: var(--transition-smooth);">  
                                <i class="fa-brands fa-telegram" style="font-size: 28px;"></i>  
                                <span style="font-size: 13.5px; font-weight: 700;">টেলিগ্রাম সাপোর্ট</span>  
                            </div>  
                        </a>  
                        <a href="https://wa.me/8801323204076" target="_blank" style="text-decoration: none;">  
                            <div style="background: #25D366; color: white; padding: 16px; border-radius: 18px; text-align: center; box-shadow: 0 6px 15px rgba(37, 211, 102, 0.35); display: flex; flex-direction: column; align-items: center; gap: 8px; transition: var(--transition-smooth);">  
                                <i class="fa-brands fa-whatsapp" style="font-size: 28px;"></i>  
                                <span style="font-size: 13.5px; font-weight: 700;">হোয়াটসঅ্যাপ চ্যাট</span>  
                            </div>  
                        </a>  
                    </div>  
  
                    <div class="task-box" style="text-align: left;">  
                        <h4 style="font-size: 15.5px; margin-bottom: 6px;">সাপোর্ট টিমকে বার্তা পাঠান</h4>  
                        <p style="font-size: 12.5px; color: var(--text-muted); margin-bottom: 16px;">আমরা ২৪ ঘণ্টার মধ্যে সমাধান দিয়ে থাকি।</p>  
                        <div class="input-group">  
                            <label>আপনার সমস্যা বিস্তারিত লিখুন</label>  
                            <textarea id="help-msg" rows="4" placeholder="এখানে লিখুন..."></textarea>  
                        </div>  
                        <button class="btn-action" onclick="submitHelp()">মেসেজ পাঠান</button>  
                    </div>  
                </div>  
  
                <!-- উইথড্র পেজ -->  
                <div id="view-withdraw" class="page-view">  
                    <button class="back-btn" onclick="openPage('home')"><i class="fa-solid fa-arrow-left"></i> ব্যাক</button>  
                    <div class="withdraw-card">  
                        <p style="font-size: 12.5px; color: rgba(255, 255, 255, 0.85); font-weight: 500;">উইথড্রযোগ্য ব্যালেন্স</p>  
                        <h1 style="color: white; margin-bottom: 18px; font-size: 32px;">৳ <span class="val-balance">0.00</span></h1>  
                          
                        <p style="font-size: 13.5px; font-weight: 600; color: #ffffff;">পেমেন্ট মেথড নির্বাচন করুন</p>  
                          
                        <div class="method-grid">  
                            <div class="method-item active" data-method="bkash" onclick="selectMethod(this, 'bkash')">  
                                <i class="fa-solid fa-wallet" style="color: #ffffff;"></i>  
                                <span>বিকাশ</span>  
                            </div>  
                            <div class="method-item" data-method="nagad" onclick="selectMethod(this, 'nagad')">  
                                <i class="fa-solid fa-mobile-screen-button" style="color: #ffffff;"></i>  
                                <span>নগদ</span>  
                            </div>  
                            <div class="method-item" data-method="bank" onclick="selectMethod(this, 'bank')">  
                                <i class="fa-solid fa-building-columns" style="color: #ffffff;"></i>  
                                <span>ব্যাংক</span>  
                            </div>  
                        </div>  
  
                        <div class="input-group">  
                            <label style="color:#ffffff;" id="w-num-label">বিকাশ অ্যাকাউন্ট নম্বর</label>  
                            <input type="tel" id="w-number" class="withdraw-input" placeholder="017XXXXXXXX">  
                        </div>  
                        <div class="input-group">  
                            <label style="color:#ffffff;">উইথড্র পরিমাণ (৳)</label>  
                            <input type="number" id="w-amount" class="withdraw-input" placeholder="সর্বনিম্ন ১০০ টাকা">  
                        </div>  
                        <div class="input-group">  
                            <label style="color:#ffffff;">সিকিউরিটি পিন (PIN)</label>  
                            <input type="password" id="w-pin" class="withdraw-input" maxlength="4" placeholder="****">  
                        </div>  
                          
                        <button class="btn-withdraw-action" onclick="processWithdraw()">উইথড্র নিশ্চিত করুন</button>  
                    </div>  
                </div>  
  
                <!-- ভিডিও পেজ -->  
                <div id="view-video" class="page-view">  
                    <button class="back-btn" onclick="openPage('home')"><i class="fa-solid fa-arrow-left"></i> ব্যাক</button>  
                    <h3>ভিডিও দেখে আয়</h3>  
                    <div class="task-box">  
                        <div style="font-size: 45px; color: var(--primary-purple); margin-bottom: 12px;"><i class="fa-solid fa-circle-play"></i></div>  
                        <h4 style="font-size: 17px;">স্পনসর ভিডিও #১</h4>  
                        <p style="color:var(--text-muted); font-size:13.5px; margin: 8px 0 18px 0;">৩০ সেকেন্ড সম্পন্ন করুন এবং পাবেন ৳১০</p>  
                        <button class="btn-action" onclick="addMoney(10, 'ভিডিও দেখা সম্পন্ন! ৳১০ যোগ হয়েছে।')">ভিডিও দেখুন</button>  
                    </div>  
                </div>  
  
                <!-- ক্যাপচা পেজ -->  
                <div id="view-captcha" class="page-view">  
                    <button class="back-btn" onclick="openPage('home')"><i class="fa-solid fa-arrow-left"></i> ব্যাক</button>  
                    <h3>টাইপিং ও ক্যাপচা সলভ</h3>  
                    <div class="task-box" style="padding-top: 30px; padding-bottom: 30px;">  
                        <div style="background: #f1f5f9; padding: 20px 16px; border-radius: 18px; margin-bottom: 18px; border: 2px dashed var(--primary-purple); display: flex; align-items: center; justify-content: center; min-height: 70px;">  
                            <h2 id="captcha-code" style="letter-spacing: 10px; color:var(--primary-purple); font-family: monospace; font-size: 28px; line-height: 1;">A8K9P</h2>  
                        </div>  
                        <div class="input-group" style="margin-bottom: 22px;">  
                            <input type="text" id="captcha-input" placeholder="উপরের কোডটি এখানে টাইপ করুন" style="text-align:center; font-weight: bold; letter-spacing: 4px; padding: 18px; font-size: 17px; border-radius: 18px; border: 2px solid var(--primary-purple); background: #ffffff; min-height: 68px; outline: none; width: 100%;">  
                        </div>  
                        <button class="btn-action" style="padding: 16px; font-size: 16.5px;" onclick="verifyCaptcha()">ক্যাপচা সাবমিট</button>  
                    </div>  
                </div>  
  
                <!-- রেফার পেজ -->  
                <div id="view-refer" class="page-view">  
                    <button class="back-btn" onclick="openPage('home')"><i class="fa-solid fa-arrow-left"></i> ব্যাক</button>  
                      
                    <div class="referral-hero-card">  
                        <div class="referral-hero-icon"><i class="fa-solid fa-gift"></i></div>  
                        <div class="referral-hero-text">  
                            <h3>প্রতি সফল রেফারে বোনাস</h3>  
                            <p>৳ ৫০</p>  
                        </div>  
                    </div>  
  
                    <div class="ref-box-container">  
                        <label style="font-weight: 700; font-size: 13.5px; color: var(--text-dark);">আপনার সিকিউর রেফারেল লিংক</label>  
                        <div class="ref-input-group">  
                            <input type="text" id="ref-link" value="https://easyearn.com/ref?user=0000" readonly>  
                            <button class="ref-copy-btn" onclick="copyRefLink()">কপি</button>  
                        </div>  
                    </div>  
  
                    <div style="margin-top: 18px;">  
                        <h3 style="font-size: 16.5px; margin-bottom: 14px; color: var(--text-dark); display: flex; align-items: center; gap: 8px;"><i class="fa-solid fa-trophy" style="color: #f59e0b;"></i> শীর্ষ রেফিলারগণ</h3>  
                        <div class="leaderboard-list">  
                            <div class="leaderboard-item">  
                                <div class="rank-badge rank-1">১</div>  
                                <div style="flex: 1;">  
                                    <h4 style="font-size: 14.5px; font-weight: 700; color: var(--text-dark);">ফাহিম আহমেদ</h4>  
                                    <p style="font-size: 11.5px; color: var(--text-muted);">১১২ জন রেফার</p>  
                                </div>  
                                <span style="font-weight: 700; color: var(--green); font-size: 14.5px;">+৳ ৫,৬০০</span>  
                            </div>  
                            <div class="leaderboard-item">  
                                <div class="rank-badge rank-2">২</div>  
                                <div style="flex: 1;">  
                                    <h4 style="font-size: 14.5px; font-weight: 700; color: var(--text-dark);">তানভীর হাসান</h4>  
                                    <p style="font-size: 11.5px; color: var(--text-muted);">৮৫ জন রেফার</p>  
                                </div>  
                                <span style="font-weight: 700; color: var(--green); font-size: 14.5px;">+৳ ৪,২৫০</span>  
                            </div>  
                            <div class="leaderboard-item">  
                                <div class="rank-badge rank-3">৩</div>  
                                <div style="flex: 1;">  
                                    <h4 style="font-size: 14.5px; font-weight: 700; color: var(--text-dark);">সাকিব আল হাসান</h4>  
                                    <p style="font-size: 11.5px; color: var(--text-muted);">৬০ জন রেফার</p>  
                                </div>  
                                <span style="font-weight: 700; color: var(--green); font-size: 14.5px;">+৳ ৩,০০০</span>  
                            </div>  
                        </div>  
                    </div>  
                </div>  
  
            </div>  
  
            <!-- নিচের নেভিগেশন বার -->  
            <div class="bottom-nav">  
                <div class="nav-item active" id="nav-home" onclick="openPage('home')">  
                    <i class="fa-solid fa-house"></i>  
                    <span>হোম</span>  
                </div>  
                <div class="nav-item" id="nav-report" onclick="openPage('report')">  
                    <i class="fa-solid fa-chart-column"></i>  
                    <span>রিপোর্ট</span>  
                </div>  
                <div class="nav-item" id="nav-emergency" onclick="openPage('emergency')">  
                    <i class="fa-solid fa-bell"></i>  
                    <span>জরুরি নোটিফিকেশন</span>  
                </div>  
                <div class="nav-item" id="nav-withdraw" onclick="openPage('withdraw')">  
                    <i class="fa-solid fa-sack-dollar"></i>  
                    <span>উইথড্র</span>  
                </div>  
                <div class="nav-item" id="nav-profile" onclick="openPage('profile')">  
                    <i class="fa-solid fa-user"></i>  
                    <span>প্রোফাইল</span>  
                </div>  
            </div>  
        </div>  
    </div>  
  
    <script>  
        const supabaseUrl = 'https://fxyvnpuznrcsytwgvcqu.supabase.co';  
        const supabaseKey = 'sb_publishable_HjZRA1YBxkITaOC7F6XmOg_5ukHe1XN';  
        const _supabase = supabase.createClient(supabaseUrl, supabaseKey);  
  
        const SecurityModule = (function() {  
            let _csrfToken = '';  
            let _failedAttempts = 0;  
  
            return {  
                generateToken: function() {  
                    _csrfToken = 'SEC-TOK-' + Math.random().toString(36).substring(2) + Date.now();  
                    document.getElementById('sec-csrf-token').value = _csrfToken;  
                },  
                verifyToken: function() {  
                    const currentToken = document.getElementById('sec-csrf-token').value;  
                    return currentToken === _csrfToken;  
                },  
                sanitize: function(input) {  
                    const el = document.createElement('div');  
                    el.innerText = input;  
                    return el.innerHTML.trim();  
                },  
                registerFailedAttempt: function() {  
                    _failedAttempts++;  
                    if (_failedAttempts >= 4) {  
                        showToast("সিকিউরিটি এলার্ট: বারবার ভুল ইনপুটের কারণে সিস্টেম থেকে সাময়িকভাবে ব্লক করা হয়েছে!", true);  
                        SecurityModule.logout();  
                    }  
                },  
                resetAttempts: function() { _failedAttempts = 0; },  
                logout: function() {  
                    showLoader(true);  
                    setTimeout(() => {  
                        document.getElementById('main-app').style.display = 'none';  
                        document.getElementById('auth-screen').style.display = 'flex';  
                        openPage('home');  
                        showLoader(false);  
                    }, 500);  
                }  
            };  
        })();  
  
        let currentBalance = 0.00;  
        let historyLogs = [];  
        let currentUserPhone = '';  
        let selectedWithdrawMethod = 'bkash';  
  
        window.onload = function() {  
            const savedPhone = localStorage.getItem('saved_login_phone');  
            if (savedPhone) {  
                document.getElementById('login-phone').value = savedPhone;  
                document.getElementById('remember-me').checked = true;  
            }  
        };  
  
        function showLoader(show) {  
            const loader = document.getElementById('app-loader');  
            if (show) loader.classList.add('active');  
            else loader.classList.remove('active');  
        }  
  
        function triggerConfetti() {  
            if (typeof confetti === 'function') {  
                confetti({  
                    particleCount: 100,  
                    spread: 70,  
                    origin: { y: 0.6 }  
                });  
            }  
        }  
  
        function togglePass(fieldId, iconEl) {  
            const field = document.getElementById(fieldId);  
            if (field.type === "password") {  
                field.type = "text";  
                iconEl.classList.remove("fa-eye-slash");  
                iconEl.classList.add("fa-eye");  
            } else {  
                field.type = "password";  
                iconEl.classList.remove("fa-eye");  
                iconEl.classList.add("fa-eye-slash");  
            }  
        }  
  
        // ENHANCED AI CHAT SYSTEM WITH TYPING EFFECT & CONTEXTUAL MEMORY  
        let aiChatHistory = [];  
  
        function openAIChat() {  
            const modal = document.getElementById('ai-chat-modal');  
            modal.style.display = 'flex';  
            const chatBody = document.getElementById('ai-chat-messages');  
            chatBody.scrollTop = chatBody.scrollHeight;  
        }  
  
        function closeAIChat() {  
            document.getElementById('ai-chat-modal').style.display = 'none';  
        }  
  
        function handleAIPress(e) {  
            if (e.key === 'Enter') {  
                sendAIMessage();  
            }  
        }  
  
        function sendAIMessage() {  
            const inputField = document.getElementById('ai-user-input');  
            const userText = inputField.value.trim();  
            if (!userText) return;  
  
            const chatBody = document.getElementById('ai-chat-messages');  
  
            // Append User Message  
            const userMsgDiv = document.createElement('div');  
            userMsgDiv.className = 'ai-message user';  
            userMsgDiv.innerText = userText;  
            chatBody.appendChild(userMsgDiv);  
  
            inputField.value = '';  
            chatBody.scrollTop = chatBody.scrollHeight;  
  
            // Save to history  
            aiChatHistory.push({ role: 'user', text: userText });  
  
            // Show Typing Indicator  
            const typingDiv = document.createElement('div');  
            typingDiv.className = 'ai-typing-indicator';  
            typingDiv.id = 'ai-typing';  
            typingDiv.innerHTML = '<div class="ai-typing-dot"></div><div class="ai-typing-dot"></div><div class="ai-typing-dot"></div>';  
            chatBody.appendChild(typingDiv);  
            chatBody.scrollTop = chatBody.scrollHeight;  
  
            // Dynamic Adaptive Delay based on message length for realistic AI typing feel  
            const responseDelay = Math.min(Math.max(userText.length * 20, 600), 1500);  
  
            setTimeout(() => {  
                const typingElem = document.getElementById('ai-typing');  
                if (typingElem) typingElem.remove();  
  
                const botResponse = getAdvancedSmartAIResponse(userText);  
                  
                const botMsgDiv = document.createElement('div');  
                botMsgDiv.className = 'ai-message bot';  
                botMsgDiv.innerHTML = formatAIResponseText(botResponse);  
                chatBody.appendChild(botMsgDiv);  
                chatBody.scrollTop = chatBody.scrollHeight;  
  
                aiChatHistory.push({ role: 'bot', text: botResponse });  
            }, responseDelay);  
        }  
  
        function formatAIResponseText(text) {  
            return text.replace(/\n/g, '<br>');  
        }  
  
        function getAdvancedSmartAIResponse(query) {  
            const q = query.toLowerCase();  
            if (q.includes('টাকা') || q.includes('উইথড্র') || q.includes('withdraw') || q.includes('balance') || q.includes('পেমেন্ট') || q.includes('ટકા')) {  
                return "💰 টাকা উইথড্র করার নিয়ম:\n১. নিচের নেভিগেশন বা হোম থেকে 'উইথড্র' অপশনে যান।\n২. বিকাশ, নগদ বা ব্যাংক সিলেক্ট করুন।\n৩. আপনার সঠিক নম্বর, টাকার পরিমাণ (কমপক্ষে ১০০ টাকা) এবং ৪ ডিজিটের সিকিউরিটি পিন দিয়ে 'উইথড্র নিশ্চিত করুন' বাটনে ক্লিক করুন। ২৪ ঘণ্টার মধ্যে পেমেন্ট পেয়ে যাবেন!";  
            } else if (q.includes('কাজ') || q.includes('task') || q.includes('income') || q.includes('আয়') || q.includes('কিভাবে কাজ') || q.includes('video') || q.includes('ইনকাম')) {  
                return "🛠️ EasyEarn প্ল্যাটফর্মে কাজ করার দুর্দান্ত মাধ্যমসমূহ:\n• ভিডিও টাস্ক: স্পনসর ভিডিও দেখে আয়।\n• সোশ্যাল টাস্ক: টেলিগ্রাম, টিকটক ও ইউটিউব সাবস্ক্রাইব/ফলো করে।\n• কুইজ ম্যাচ: সাধারণ জ্ঞানের সঠিক উত্তর দিয়ে।\n• সার্ভে কাজ: মতামত শেয়ার করে।\n• ক্যাপচা ও টাইপিং: কোড টাইপ করে তাৎক্ষণিক আয়।";  
            } else if (q.includes('রেফার') || q.includes('refer') || q.includes('বন্ধুদের') || q.includes('invite')) {  
                return "🎁 রেফার করে আয়:\nপ্রতিটি সফল রেফারে আপনি পাবেন আকর্ষণীয় ৫০ টাকা বোনাস! 'রেফার ও ইনকাম' পেজ থেকে আপনার সিকিউর লিংকটি কপি করে বন্ধুদের সাথে শেয়ার করুন।";  
            } else if (q.includes('পাসওয়ার্ড') || q.includes('password') || q.includes('ভুলে') || q.includes('forgot')) {  
                return "🔑 পাসওয়ার্ড রিকভারি:\nলগইন পেজে থাকা 'পাসওয়ার্ড ভুলে গেছেন?' লিঙ্কে ক্লিক করে আপনার রেজিস্টার্ড মোবাইল নম্বর দিয়ে খুব সহজেই নতুন পাসওয়ার্ড সেট করতে পারবেন।";  
            } else if (q.includes('হেল্প') || q.includes('support') || q.includes('যোগাযোগ') || q.includes('help') || q.includes('admin') || q.includes('সাপোর্ট')) {  
                return "📞 লাইভ সাপোর্ট:\nআমাদের ২৪/৭ হেল্প সেন্টার থেকে সরাসরি টেলিগ্রাম বা হোয়াটসঅ্যাপ সাপোর্টে যোগাযোগ করতে পারেন অথবা প্রোফাইল থেকে সাপোর্ট মেসেজ পাঠাতে পারেন।";  
            } else if (q.includes('সিকিউরিটি') || q.includes('security') || q.includes('ব্যান') || q.includes('ban') || q.includes('নিয়ম')) {  
                return "🛡️ সিকিউরিটি ও নিয়মকানুন:\nআমাদের প্ল্যাটফর্মে মাল্টিপল অ্যাকাউন্ট খোলা বা ভুয়া উপায়ে কাজ করা সম্পূর্ণ নিষিদ্ধ। নিয়ম অমান্য করলে সিস্টেম স্বয়ংক্রিয়ভাবে অ্যাকাউন্ট ব্যান করতে পারে। নিরাপদে কাজ করুন ও পেমেন্ট নিন!";  
            } else if (q.includes('হ্যালো') || q.includes('hi') || q.includes('hello') || q.includes('salam') || q.includes('আসসালামু') || q.includes('কেমন')) {  
                return "👋 ওয়ালাইকুমুস সালাম / হ্যালো! EasyEarn প্রিমিয়াম প্ল্যাটফর্মে আপনাকে স্বাগতম। আজ আপনাকে কীভাবে সহায়তা করতে পারি বলুন?";  
            } else {  
                return "🤖 আপনার প্রশ্নটি আমি খুব মনোযোগ দিয়ে শুনেছি। এই বিষয়ে বিস্তারিত তথ্য বা সরাসরি সহায়তার জন্য আমাদের 'হেল্প সেন্টার' অপশনে গিয়ে টেলিগ্রাম বা হোয়াটসঅ্যাপ সাপোর্টে যোগাযোগ করতে পারেন। আমি সব সময় আপনার সেবায় প্রস্তুত আছি!";  
            }  
        }  
  
        async function handleSignup(e) {  
            e.preventDefault();  
            showLoader(true);  
            const rawName = document.getElementById('reg-name').value;  
            const rawPhone = document.getElementById('reg-phone').value;  
            const rawEmail = document.getElementById('reg-email').value;  
            const rawPass = document.getElementById('reg-pass').value;  
            const rawCPass = document.getElementById('reg-cpass').value;  
  
            const name = SecurityModule.sanitize(rawName);  
            const phone = SecurityModule.sanitize(rawPhone);  
            const email = SecurityModule.sanitize(rawEmail);  
  
            if (phone.length !== 11 || isNaN(phone)) {  
                showLoader(false);  
                showToast('সঠিক ১১ ডিজিটের মোবাইল নম্বর দিন!', true);  
                return;  
            }  
            if (rawPass.length < 6) {  
                showLoader(false);  
                showToast('পাসওয়ার্ড অন্তত ৬ ডিজিট হতে হবে!', true);  
                return;  
            }  
            if (rawPass !== rawCPass) {  
                showLoader(false);  
                showToast('পাসওয়ার্ড এবং কনফার্ম পাসওয়ার্ড মিলছে না!', true);  
                return;  
            }  
  
            const { data: existingUser } = await _supabase  
                .from('users')  
                .select('*')  
                .eq('phone', phone)  
                .maybeSingle();  
  
            if (existingUser) {  
                showLoader(false);  
                showToast('এই নম্বরটি আগেই নিবন্ধিত হয়েছে!', true);  
                return;  
            }  
  
            const { error } = await _supabase  
                .from('users')  
                .insert([{ name: name, phone: phone, email: email, pass: rawPass, balance: 0.00 }]);  
  
            if (error) {  
                showLoader(false);  
                showToast('রেজিস্ট্রেশনে সমস্যা হয়েছে: ' + error.message, true);  
                return;  
            }  
  
            showLoader(false);  
            loginUser(name, phone, 0.00);  
            triggerConfetti();  
            showToast('অ্যাকাউন্ট সফলভাবে তৈরি হয়েছে!');  
        }  
  
        async function handleLogin(e) {  
            e.preventDefault();  
            showLoader(true);  
            const phone = SecurityModule.sanitize(document.getElementById('login-phone').value);  
            const pass = document.getElementById('login-pass').value;  
            const rememberMe = document.getElementById('remember-me').checked;  
  
            const { data: user, error } = await _supabase  
                .from('users')  
                .select('*')  
                .eq('phone', phone)  
                .maybeSingle();  
  
            if (error || !user) {  
                showLoader(false);  
                SecurityModule.registerFailedAttempt();  
                showToast('অ্যাকাউন্ট পাওয়া যায়নি!', true);  
                return;  
            }  
  
            if (user.pass !== pass) {  
                showLoader(false);  
                SecurityModule.registerFailedAttempt();  
                showToast('ভুল পাসওয়ার্ড!', true);  
                return;  
            }  
  
            if (rememberMe) {  
                localStorage.setItem('saved_login_phone', phone);  
            } else {  
                localStorage.removeItem('saved_login_phone');  
            }  
  
            showLoader(false);  
            SecurityModule.resetAttempts();  
            loginUser(user.name, phone, user.balance || 0.00);  
            showToast('সফলভাবে প্রবেশ করেছেন!');  
        }  
  
        function showForgotModal() {  
            const phoneInput = prompt("আপনার রেজিস্টার্ড ১১ ডিজিটের মোবাইল নম্বরটি দিন:");  
            if (phoneInput) {  
                if (phoneInput.length === 11) {  
                    showToast("পাসওয়ার্ড রিকভারি নির্দেশনা আপনার নম্বরে পাঠানো হয়েছে!");  
                } else {  
                    showToast("সঠিক ১১ ডিজিটের নম্বর দিন!", true);  
                }  
            }  
        }  
  
        function loginUser(name, phone, balance) {  
            currentUserPhone = phone;  
            currentBalance = balance;  
            SecurityModule.generateToken();  
            document.getElementById('display-name').innerText = name;  
            document.getElementById('display-phone').innerText = phone;  
            document.getElementById('ref-link').value = `https://easyearn.com/ref?user=${phone.substring(7)}`;  
            document.getElementById('auth-screen').style.display = 'none';  
            document.getElementById('main-app').style.display = 'flex';  
            updateBalanceUI();  
            renderQuiz();  
        }  
  
        function showToast(msg, isError = false) {  
            const toast = document.getElementById('toast');  
            toast.innerText = msg;  
            toast.style.background = isError ? 'linear-gradient(135deg, #ef4444, #dc2626)' : 'linear-gradient(135deg, #10b981, #059669)';  
            toast.classList.add('show');  
            setTimeout(() => { toast.classList.remove('show'); }, 3000);  
        }  
  
        function switchAuthTab(type) {  
            document.getElementById('signup-container').style.display = type === 'signup' ? 'block' : 'none';  
            document.getElementById('login-container').style.display = type === 'login' ? 'block' : 'none';  
        }  
  
        const quizList = [  
            { q: "বাংলাদেশের রাজধানী কোনটি?", options: ["ঢাকা", "চট্টগ্রাম", "সিলেট", "খুলনা"], ans: "ঢাকা" },  
            { q: "সাইবার সুরক্ষায় পাসওয়ার্ডের সর্বনিম্ন দৈর্ঘ্য কত হওয়া ভালো?", options: ["৪", "৬", "৮", "২"], ans: "৮" },  
            { q: "২ + ২ × ২ = কত?", options: ["৮", "৬", "৪", "১০"], ans: "৬" }  
        ];  
        let currentQuizIndex = 0;  
  
        function renderQuiz() {  
            const qData = quizList[currentQuizIndex];  
            document.getElementById('quiz-question').innerText = qData.q;  
            const optContainer = document.getElementById('quiz-options');  
            optContainer.innerHTML = '';  
  
            qData.options.forEach(opt => {  
                const btn = document.createElement('button');  
                btn.className = 'btn-action';  
                btn.style.background = '#f1f5f9';  
                btn.style.color = '#1e293b';  
                btn.style.marginBottom = '12px';  
                btn.style.boxShadow = '0 6px 15px rgba(0,0,0,0.03)';  
                btn.style.border = '1px solid var(--border-color)';  
                btn.innerText = opt;  
                btn.onclick = () => checkQuiz(opt, qData.ans);  
                optContainer.appendChild(btn);  
            });  
        }  
  
        function checkQuiz(selected, correct) {  
            if(selected === correct) {  
                triggerConfetti();  
                addMoney(3, 'সঠিক উত্তর! ৳৩ যোগ হয়েছে।');  
            } else {  
                showToast('ভুল উত্তর! পরবর্তী প্রশ্ন আসছে...', true);  
            }  
            currentQuizIndex = (currentQuizIndex + 1) % quizList.length;  
            renderQuiz();  
        }  
  
        function submitSurvey() {  
            const txt = document.getElementById('survey-input').value;  
            if(!txt) { showToast('উত্তর প্রদান করুন!', true); return; }  
            triggerConfetti();  
            addMoney(15, 'সার্ভে জমা দেওয়ার জন্য ৳১৫ পেয়েছেন!');  
            document.getElementById('survey-input').value = '';  
            openPage('home');  
        }  
  
        function verifyCaptcha() {  
            const input = document.getElementById('captcha-input').value;  
            const code = document.getElementById('captcha-code').innerText;  
            if(input.toUpperCase() === code) {  
                triggerConfetti();  
                addMoney(3, 'ক্যাপচা সফল! ৳৩ দেওয়া হয়েছে।');  
                document.getElementById('captcha-input').value = '';  
                document.getElementById('captcha-code').innerText = Math.random().toString(36).substring(2, 7).toUpperCase();  
            } else {  
                showToast('ভুল ক্যাপচা কোড!', true);  
            }  
        }  
  
        function openPage(pageName) {  
            document.querySelectorAll('.page-view').forEach(v => v.classList.remove('active'));  
            const targetView = document.getElementById('view-' + pageName);  
            if(targetView) targetView.classList.add('active');  
  
            document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));  
            const activeNav = document.getElementById('nav-' + pageName);  
            if(activeNav) activeNav.classList.add('active');  
              
            const contentArea = document.querySelector('.content');  
            if(contentArea) contentArea.scrollTop = 0;  
        }  
  
        async function addMoney(amount, message) {  
            if (!SecurityModule.verifyToken()) {  
                showToast("সিকিউরিটি ফেইল্ড! রিলোড দিন।", true);  
                return;  
            }  
            currentBalance += amount;  
              
            if (currentUserPhone) {  
                await _supabase  
                    .from('users')  
                    .update({ balance: currentBalance })  
                    .eq('phone', currentUserPhone);  
            }  
  
            historyLogs.unshift({  
                type: message.substring(0, 22),  
                amount: amount,  
                time: new Date().toLocaleTimeString('bn-BD')  
            });  
  
            updateBalanceUI();  
            renderLogs();  
            showToast(message);  
        }  
  
        function renderLogs() {  
            const box = document.getElementById('history-list-box');  
            if (historyLogs.length === 0) return;  
              
            box.innerHTML = historyLogs.map(log => `  
                <div class="social-item">  
                    <div>  
                        <p style="font-weight:700; font-size:14.5px;">${SecurityModule.sanitize(log.type)}</p>  
                        <p style="font-size:11.5px; color:var(--text-muted);">${log.time}</p>  
                    </div>  
                    <span style="color:var(--green); font-weight:700;">+ ৳${log.amount.toFixed(2)}</span>  
                </div>  
            `).join('');  
        }  
  
        function updateBalanceUI() {  
            document.querySelectorAll('.val-balance').forEach(el => el.innerText = currentBalance.toFixed(2));  
        }  
  
        function selectMethod(el, method) {  
            selectedWithdrawMethod = method;  
            document.querySelectorAll('.method-item').forEach(m => m.classList.remove('active'));  
            el.classList.add('active');  
  
            const labelEl = document.getElementById('w-num-label');  
            if (method === 'bkash') {  
                labelEl.innerText = "বিকাশ অ্যাকাউন্ট নম্বর";  
            } else if (method === 'nagad') {  
                labelEl.innerText = "নগদ অ্যাকাউন্ট নম্বর";  
            } else if (method === 'bank') {  
                labelEl.innerText = "ব্যাংক অ্যাকাউন্ট ও রাউটিং নম্বর";  
            }  
        }  
  
        async function processWithdraw() {  
            const num = SecurityModule.sanitize(document.getElementById('w-number').value);  
            const amt = parseFloat(document.getElementById('w-amount').value);  
            const pin = document.getElementById('w-pin').value;  
  
            if (!SecurityModule.verifyToken()) {  
                showToast('সেশন অকার্যকর!', true);  
                return;  
            }  
  
            if(!num || !amt || !pin) { showToast('সবগুলো তথ্য সঠিকভাবে দিন!', true); return; }  
            if(amt < 100) { showToast('সর্বনিম্ন উইথড্র ১০০ টাকা!', true); return; }  
            if(amt > currentBalance) {   
                showToast(`অপর্যাপ্ত ব্যালেন্স! আপনার ব্যালেন্স ৳ ${currentBalance.toFixed(2)}`, true);   
                return;   
            }  
  
            showLoader(true);  
            currentBalance -= amt;  
              
            if (currentUserPhone) {  
                await _supabase  
                    .from('users')  
                    .update({ balance: currentBalance })  
                    .eq('phone', currentUserPhone);  
            }  
  
            setTimeout(() => {  
                showLoader(false);  
                triggerConfetti();  
                updateBalanceUI();  
                document.getElementById('w-number').value = ``;  
                document.getElementById('w-amount').value = ``;  
                document.getElementById('w-pin').value = ``;  
                showToast('উইথড্র রিকোয়েস্ট সফলভাবে জমা হয়েছে!');  
            }, 600);  
        }  
  
        function copyRefLink() {  
            const link = document.getElementById('ref-link');  
            link.select();  
            document.execCommand('copy');  
            showToast('রেফারেল লিঙ্ক সফলভাবে কপি করা হয়েছে!');  
        }  
  
        async function submitHelp() {  
            const rawMsg = document.getElementById('help-msg').value;  
            if(!rawMsg.trim()) {   
                showToast('দয়া করে আপনার সমস্যাটি লিখুন!', true);   
                return;   
            }  
  
            if(!currentUserPhone) {  
                showToast('লগইন করা অবস্থায় মেসেজ পাঠাতে হবে!', true);  
                return;  
            }  
  
            showLoader(true);  
            const messageText = SecurityModule.sanitize(rawMsg);  
  
            const { error } = await _supabase  
                .from('support_messages')  
                .insert([  
                    { phone: currentUserPhone, message: messageText }  
                ]);  
  
            showLoader(false);  
            if (error) {  
                showToast('বার্তা পাঠাতে সমস্যা হয়েছে: ' + error.message, true);  
                return;  
            }  
  
            showToast('সাপোর্ট টিমকে সফলভাবে বার্তা পাঠানো হয়েছে!');  
            document.getElementById('help-msg').value = ``;  
        }  
    </script>  
</body>  
</html>  

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Thiago Moabi | TM Dev</title>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Fira+Code:wght@300;400;600;700&family=Inter:wght@400;600;900&display=swap');

    :root {
      --bg: #09090b;
      --bg-panel: #18181b;
      --text-main: #f4f4f5;
      --text-muted: #a1a1aa;
      --accent-blue: #3b82f6;
      --accent-glow: rgba(59, 130, 246, 0.5);
      --terminal-green: #10b981;
      --border: #27272a;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      background-color: var(--bg);
      color: var(--text-main);
      font-family: 'Inter', sans-serif;
      overflow-x: hidden;
      line-height: 1.6;
      background-image: 
        radial-gradient(circle at 15% 50%, rgba(59, 130, 246, 0.08) 0%, transparent 50%),
        radial-gradient(circle at 85% 30%, rgba(16, 185, 129, 0.05) 0%, transparent 50%);
    }

    /* --- Animations --- */
    @keyframes float {
      0% { transform: translateY(0px); }
      50% { transform: translateY(-10px); }
      100% { transform: translateY(0px); }
    }

    @keyframes scanline {
      0% { transform: translateY(-100%); opacity: 0; }
      50% { opacity: 0.2; }
      100% { transform: translateY(100vh); opacity: 0; }
    }

    @keyframes pulse-glow {
      0%, 100% { box-shadow: 0 0 15px var(--accent-glow); }
      50% { box-shadow: 0 0 30px rgba(59, 130, 246, 0.8); }
    }

    @keyframes typing {
      from { width: 0; }
      to { width: 100%; }
    }

    @keyframes blink {
      50% { border-color: transparent; }
    }

    /* --- Layout --- */
    .container {
      max-width: 1000px;
      margin: 0 auto;
      padding: 4rem 2rem;
      position: relative;
    }

    /* Scanline overlay */
    .container::before {
      content: "";
      position: fixed;
      top: 0; left: 0; width: 100%; height: 2px;
      background: var(--accent-blue);
      animation: scanline 6s linear infinite;
      pointer-events: none;
      z-index: 9999;
    }

    /* --- Header --- */
    header {
      text-align: center;
      margin-bottom: 4rem;
    }

    .title-wrapper {
      display: inline-block;
    }

    h1 {
      font-family: 'Fira Code', monospace;
      font-size: 3.5rem;
      font-weight: 700;
      letter-spacing: -2px;
      margin-bottom: 0.5rem;
      background: linear-gradient(to right, #fff, var(--text-muted));
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      overflow: hidden;
      white-space: nowrap;
      border-right: 4px solid var(--accent-blue);
      animation: typing 2s steps(30, end), blink .75s step-end infinite;
    }

    h2 {
      font-size: 1.2rem;
      color: var(--text-muted);
      text-transform: uppercase;
      letter-spacing: 2px;
      margin-bottom: 1.5rem;
    }

    .badges {
      display: flex;
      justify-content: center;
      gap: 1rem;
      flex-wrap: wrap;
    }

    .badge {
      padding: 0.5rem 1rem;
      background: var(--bg-panel);
      border: 1px solid var(--border);
      border-radius: 6px;
      font-family: 'Fira Code', monospace;
      font-size: 0.85rem;
      color: var(--text-main);
      text-decoration: none;
      transition: all 0.3s ease;
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .badge:hover {
      border-color: var(--accent-blue);
      transform: translateY(-3px);
      box-shadow: 0 5px 15px rgba(59, 130, 246, 0.2);
    }

    /* --- Terminal Box --- */
    .terminal {
      background: #000;
      border-radius: 10px;
      border: 1px solid #333;
      padding: 1.5rem;
      font-family: 'Fira Code', monospace;
      color: var(--terminal-green);
      margin-bottom: 4rem;
      box-shadow: 0 20px 40px rgba(0,0,0,0.5);
      position: relative;
      overflow: hidden;
    }

    .terminal-header {
      display: flex;
      gap: 8px;
      margin-bottom: 1rem;
      border-bottom: 1px solid #333;
      padding-bottom: 1rem;
    }

    .dot {
      width: 12px; height: 12px; border-radius: 50%;
    }
    .dot.r { background: #ef4444; }
    .dot.y { background: #f59e0b; }
    .dot.g { background: #10b981; }

    .terminal p {
      margin-bottom: 0.5rem;
      font-size: 0.95rem;
    }
    .terminal .comment { color: #6b7280; }
    .terminal .key { color: #38bdf8; }

    /* --- Grid Cards (3D Tilt effect) --- */
    .section-title {
      font-family: 'Fira Code', monospace;
      font-size: 1.5rem;
      color: var(--accent-blue);
      margin-bottom: 1.5rem;
      display: flex;
      align-items: center;
      gap: 10px;
    }
    .section-title::before {
      content: ">>";
      color: var(--text-muted);
    }

    .grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
      gap: 2rem;
      margin-bottom: 4rem;
    }

    .card {
      background: var(--bg-panel);
      border: 1px solid var(--border);
      border-radius: 12px;
      padding: 2rem;
      transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
      position: relative;
      overflow: hidden;
      transform-style: preserve-3d;
    }

    /* Pseudo 3D Hover & Glow */
    .card:hover {
      transform: translateY(-10px) scale(1.02);
      border-color: var(--accent-blue);
      box-shadow: 0 15px 30px rgba(0, 0, 0, 0.5), 0 0 20px rgba(59, 130, 246, 0.2);
    }
    .card::after {
      content: '';
      position: absolute;
      top: 0; left: -100%;
      width: 50%; height: 100%;
      background: linear-gradient(to right, transparent, rgba(255,255,255,0.05), transparent);
      transform: skewX(-20deg);
      transition: left 0.7s ease;
    }
    .card:hover::after {
      left: 150%;
    }

    .card h3 {
      font-size: 1.25rem;
      margin-bottom: 1rem;
      color: #fff;
    }
    .card ul {
      list-style: none;
      color: var(--text-muted);
      font-size: 0.95rem;
    }
    .card ul li {
      margin-bottom: 0.5rem;
      display: flex;
      align-items: flex-start;
      gap: 8px;
    }
    .card ul li::before {
      content: "▹";
      color: var(--accent-blue);
    }

    /* --- Tech Stack (Floating) --- */
    .tech-stack {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 1rem;
      margin-bottom: 4rem;
    }
    .tech-stack img {
      height: 28px;
      border-radius: 4px;
      animation: float 4s ease-in-out infinite;
    }
    .tech-stack img:nth-child(2) { animation-delay: 0.5s; }
    .tech-stack img:nth-child(3) { animation-delay: 1s; }
    .tech-stack img:nth-child(4) { animation-delay: 1.5s; }
    .tech-stack img:nth-child(5) { animation-delay: 2s; }

    /* --- GitHub Stats Embeds --- */
    .stats-container {
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 2rem;
      margin-bottom: 4rem;
      animation: pulse-glow 4s infinite;
      background: var(--bg-panel);
      padding: 2rem;
      border-radius: 12px;
      border: 1px solid var(--border);
    }
    .stats-container img {
      max-width: 100%;
      border-radius: 8px;
    }
  </style>
</head>
<body>

  <div class="container">
    <header>
      <div class="title-wrapper">
        <h1>THIAGO MOABI</h1>
      </div>
      <h2>Software Engineer & Automation Architect</h2>
      <div class="badges">
        <a href="https://tmdev-one.vercel.app" target="_blank" class="badge">
          ⌬ Portfolio
        </a>
        <a href="https://linkedin.com/in/thiagomoabi" target="_blank" class="badge">
          in LinkedIn
        </a>
        <a href="https://github.com/Tfreire455" target="_blank" class="badge">
          { } GitHub
        </a>
      </div>
    </header>

    <div class="terminal">
      <div class="terminal-header">
        <div class="dot r"></div>
        <div class="dot y"></div>
        <div class="dot g"></div>
      </div>

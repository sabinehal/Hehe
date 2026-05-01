<!DOCTYPE html>

<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Dark Vortex</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Rajdhani:wght@300;400;500;600;700&family=Share+Tech+Mono&display=swap');

*,*::before,*::after{margin:0;padding:0;box-sizing:border-box;}
html{scroll-behavior:smooth;}
body{
font-family:‘Rajdhani’,Arial,sans-serif;
background:#000!important;
color:#e8e8e8;
overflow-x:hidden;
min-height:100vh;
perspective:1200px;
}

/* === PARTICLE CANVAS === */
#particles{position:fixed;inset:0;z-index:0;pointer-events:none;}

/* === NAV === */
nav{
position:fixed;top:0;left:0;right:0;z-index:1000;
display:flex;align-items:center;justify-content:space-between;
padding:16px 52px;
background:rgba(0,0,0,0.88);
border-bottom:1px solid rgba(255,255,255,0.08);
backdrop-filter:blur(24px);
-webkit-backdrop-filter:blur(24px);
transform-style:preserve-3d;
}

/* 3D Logo */
.logo{display:flex;align-items:center;gap:14px;text-decoration:none;transform-style:preserve-3d;}
.logo-img-wrap{
position:relative;width:44px;height:44px;
transform-style:preserve-3d;
animation:logoSpin3d 8s ease-in-out infinite;
}
@keyframes logoSpin3d{
0%{transform:rotateY(0deg) rotateX(0deg);}
25%{transform:rotateY(15deg) rotateX(8deg);}
50%{transform:rotateY(0deg) rotateX(0deg);}
75%{transform:rotateY(-15deg) rotateX(-8deg);}
100%{transform:rotateY(0deg) rotateX(0deg);}
}
.logo-img{
width:44px;height:44px;border-radius:50%;object-fit:cover;
border:1.5px solid rgba(255,255,255,0.5);
box-shadow:0 0 16px rgba(255,255,255,0.3),0 0 40px rgba(255,255,255,0.12),0 8px 20px rgba(0,0,0,0.8);
display:block;
}
.logo-img-wrap::after{
content:’’;position:absolute;bottom:-6px;left:50%;transform:translateX(-50%);
width:30px;height:6px;
background:radial-gradient(ellipse,rgba(255,255,255,0.2) 0%,transparent 70%);
border-radius:50%;
filter:blur(3px);
}
.logo-text{
font-family:‘Bebas Neue’,Impact,sans-serif;font-size:22px;
letter-spacing:3px;color:#fff;
text-shadow:0 0 14px rgba(255,255,255,0.5);
animation:textPulse 4s ease-in-out infinite;
}
@keyframes textPulse{
0%,100%{text-shadow:0 0 14px rgba(255,255,255,0.5),0 0 30px rgba(255,255,255,0.1);}
50%{text-shadow:0 0 20px rgba(255,255,255,0.8),0 0 50px rgba(255,255,255,0.2);}
}

.nav-links{display:flex;gap:40px;list-style:none;}
.nav-links a{
font-family:‘Rajdhani’,Arial,sans-serif;font-size:13px;font-weight:600;
color:#777;text-decoration:none;letter-spacing:2px;text-transform:uppercase;
transition:all 0.3s;position:relative;
}
.nav-links a::after{
content:’’;position:absolute;bottom:-4px;left:0;right:0;height:1px;
background:#fff;transform:scaleX(0);transform-origin:center;
transition:transform 0.3s;
box-shadow:0 0 8px rgba(255,255,255,0.6);
}
.nav-links a:hover{color:#fff;text-shadow:0 0 10px rgba(255,255,255,0.6);}
.nav-links a:hover::after{transform:scaleX(1);}

.nav-cta{
font-family:‘Rajdhani’,Arial,sans-serif;font-size:13px;font-weight:700;
letter-spacing:2px;text-transform:uppercase;padding:10px 26px;
background:#fff;color:#000;border:none;border-radius:24px;
cursor:pointer;text-decoration:none;transition:all 0.3s;
box-shadow:0 0 14px rgba(255,255,255,0.25),0 0 40px rgba(255,255,255,0.1);
transform:perspective(400px) translateZ(0);
}
.nav-cta:hover{
transform:perspective(400px) translateZ(12px) translateY(-2px);
box-shadow:0 0 28px rgba(255,255,255,0.45),0 0 70px rgba(255,255,255,0.15),0 12px 30px rgba(0,0,0,0.5);
}

/* === HERO === */
.hero{
position:relative;min-height:100vh;background:#000;
display:flex;flex-direction:column;align-items:center;justify-content:center;
text-align:center;padding:120px 24px 80px;overflow:hidden;
transform-style:preserve-3d;
}

/* Vortex rings */
.vortex-bg{position:absolute;inset:0;display:flex;align-items:center;justify-content:center;pointer-events:none;}
.vortex-ring{
position:absolute;border-radius:50%;
border:1px solid rgba(255,255,255,0.06);
animation:expandFade 7s ease-out infinite;
}
.vortex-ring:nth-child(1){width:200px;height:200px;animation-delay:0s}
.vortex-ring:nth-child(2){width:420px;height:420px;animation-delay:1.4s}
.vortex-ring:nth-child(3){width:640px;height:640px;animation-delay:2.8s}
.vortex-ring:nth-child(4){width:860px;height:860px;animation-delay:4.2s}
.vortex-ring:nth-child(5){width:1080px;height:1080px;animation-delay:5.6s}
@keyframes expandFade{
0%{opacity:0;transform:scale(0.88) rotateX(60deg);}
20%{opacity:0.2;}
100%{opacity:0;transform:scale(1.1) rotateX(0deg);}
}

.hero-badge{
position:relative;z-index:1;
display:inline-flex;align-items:center;gap:8px;padding:6px 20px;
border:1px solid rgba(255,255,255,0.3);border-radius:20px;
font-family:‘Share Tech Mono’,monospace;font-size:11px;
color:rgba(255,255,255,0.6);letter-spacing:3px;text-transform:uppercase;
margin-bottom:40px;
animation:fadeUp 0.8s ease both, badgeGlow 3s ease-in-out infinite 1s;
}
@keyframes badgeGlow{
0%,100%{box-shadow:0 0 8px rgba(255,255,255,0.08);}
50%{box-shadow:0 0 20px rgba(255,255,255,0.2),0 0 40px rgba(255,255,255,0.08);}
}

/* 3D PFP */
.pfp-wrap{
position:relative;z-index:1;width:220px;height:220px;
margin:0 auto 52px;
transform-style:preserve-3d;
animation:pfpFloat 6s ease-in-out infinite;
}
@keyframes pfpFloat{
0%,100%{transform:translateY(0px) rotateY(0deg) rotateX(0deg);}
25%{transform:translateY(-12px) rotateY(8deg) rotateX(4deg);}
50%{transform:translateY(-6px) rotateY(0deg) rotateX(0deg);}
75%{transform:translateY(-14px) rotateY(-8deg) rotateX(-4deg);}
}
.pfp-shadow{
position:absolute;bottom:-20px;left:50%;transform:translateX(-50%);
width:160px;height:20px;
background:radial-gradient(ellipse,rgba(255,255,255,0.15) 0%,transparent 70%);
border-radius:50%;filter:blur(8px);
animation:shadowPulse 6s ease-in-out infinite;
}
@keyframes shadowPulse{
0%,100%{transform:translateX(-50%) scaleX(1);opacity:0.6;}
25%{transform:translateX(-50%) scaleX(0.7);opacity:0.2;}
75%{transform:translateX(-50%) scaleX(0.65);opacity:0.15;}
}
.pfp-ring1{
position:absolute;inset:-20px;border-radius:50%;
border:1px solid rgba(255,255,255,0.15);
box-shadow:0 0 30px rgba(255,255,255,0.08);
animation:spinR 12s linear infinite;
}
.pfp-ring2{
position:absolute;inset:-10px;border-radius:50%;
border:1px solid rgba(255,255,255,0.22);
box-shadow:0 0 18px rgba(255,255,255,0.15);
animation:spinR 7s linear infinite reverse;
}
.pfp-ring3{
position:absolute;inset:-32px;border-radius:50%;
border:1px dashed rgba(255,255,255,0.06);
animation:spinR 20s linear infinite;
}
@keyframes spinR{from{transform:rotate(0deg)}to{transform:rotate(360deg)}}
.hero-pfp{
width:220px;height:220px;border-radius:50%;object-fit:cover;object-position:center top;
border:2px solid rgba(255,255,255,0.6);display:block;position:relative;z-index:1;
box-shadow:0 0 0 1px rgba(255,255,255,0.1),0 0 40px rgba(255,255,255,0.28),0 0 100px rgba(255,255,255,0.12),0 0 200px rgba(255,255,255,0.05);
}

/* 3D Text */
.hero h1{
position:relative;z-index:1;
font-family:‘Bebas Neue’,Impact,sans-serif;
font-size:clamp(64px,12vw,130px);letter-spacing:8px;line-height:0.95;margin-bottom:8px;
animation:fadeUp 0.8s 0.1s ease both;
transform-style:preserve-3d;
}
.hero h1 .l1{
color:#fff;display:block;
text-shadow:0 0 30px rgba(255,255,255,0.45),0 0 80px rgba(255,255,255,0.18),0 4px 0 rgba(255,255,255,0.05),0 8px 0 rgba(255,255,255,0.02);
animation:titleFloat 8s ease-in-out infinite;
}
.hero h1 .l2{
display:block;color:transparent;
-webkit-text-stroke:1.5px rgba(255,255,255,0.5);
filter:drop-shadow(0 0 20px rgba(255,255,255,0.25));
animation:titleFloat 8s ease-in-out infinite 0.4s;
}
@keyframes titleFloat{
0%,100%{transform:translateY(0) rotateX(0deg);}
50%{transform:translateY(-6px) rotateX(2deg);}
}

.hero-sub{
position:relative;z-index:1;font-size:18px;font-weight:300;
color:#888;max-width:520px;margin:28px auto 52px;line-height:1.7;
animation:fadeUp 0.8s 0.2s ease both;
}
.hero-btns{position:relative;z-index:1;display:flex;gap:14px;justify-content:center;flex-wrap:wrap;animation:fadeUp 0.8s 0.3s ease both;}

/* BUTTONS */
.btn-primary{
font-family:‘Rajdhani’,Arial,sans-serif;font-size:14px;font-weight:700;
letter-spacing:2px;text-transform:uppercase;padding:16px 40px;
background:#fff;color:#000;border:none;border-radius:30px;
cursor:pointer;text-decoration:none;transition:all 0.3s;
display:inline-flex;align-items:center;gap:8px;
box-shadow:0 0 14px rgba(255,255,255,0.2),0 0 40px rgba(255,255,255,0.08);
transform:perspective(400px) translateZ(0);
}
.btn-primary:hover{
transform:perspective(400px) translateZ(16px) translateY(-3px);
box-shadow:0 0 30px rgba(255,255,255,0.4),0 0 80px rgba(255,255,255,0.15),0 16px 40px rgba(0,0,0,0.6);
}
.btn-outline{
font-family:‘Rajdhani’,Arial,sans-serif;font-size:14px;font-weight:600;
letter-spacing:2px;text-transform:uppercase;padding:16px 40px;
background:transparent;color:#fff;
border:1px solid rgba(255,255,255,0.3);border-radius:30px;
cursor:pointer;text-decoration:none;transition:all 0.3s;
display:inline-flex;align-items:center;gap:8px;
transform:perspective(400px) translateZ(0);
}
.btn-outline:hover{
background:rgba(255,255,255,0.06);border-color:rgba(255,255,255,0.55);
transform:perspective(400px) translateZ(12px) translateY(-2px);
box-shadow:0 0 20px rgba(255,255,255,0.12),0 12px 30px rgba(0,0,0,0.5);
}

/* STATS */
.stats{
position:relative;z-index:1;display:flex;justify-content:center;
padding:60px 48px;background:#050505;
border-top:1px solid rgba(255,255,255,0.07);
border-bottom:1px solid rgba(255,255,255,0.07);
}
.stat{
flex:1;max-width:220px;text-align:center;padding:0 40px;
border-right:1px solid rgba(255,255,255,0.07);
transform:perspective(600px) translateZ(0);
transition:transform 0.4s;
}
.stat:hover{transform:perspective(600px) translateZ(20px);}
.stat:last-child{border-right:none;}
.stat-num{
font-family:‘Bebas Neue’,Impact,sans-serif;font-size:54px;letter-spacing:3px;color:#fff;
text-shadow:0 0 20px rgba(255,255,255,0.4),0 0 50px rgba(255,255,255,0.15);
animation:countGlow 4s ease-in-out infinite;
}
@keyframes countGlow{
0%,100%{text-shadow:0 0 20px rgba(255,255,255,0.4),0 0 50px rgba(255,255,255,0.15);}
50%{text-shadow:0 0 30px rgba(255,255,255,0.6),0 0 80px rgba(255,255,255,0.25);}
}
.stat-label{font-family:‘Share Tech Mono’,monospace;font-size:11px;letter-spacing:2px;color:#555;text-transform:uppercase;margin-top:6px;}

/* SECTIONS */
section{
position:relative;z-index:1;padding:100px 52px;max-width:1320px;margin:0 auto;background:#000;
transform-style:preserve-3d;
}
.section-head{display:flex;align-items:center;gap:16px;margin-bottom:56px;}
.sec-icon{
width:54px;height:54px;background:#111;
border:1px solid rgba(255,255,255,0.2);border-radius:16px;
display:flex;align-items:center;justify-content:center;
box-shadow:0 0 14px rgba(255,255,255,0.07);
transition:all 0.4s;
transform:perspective(300px) translateZ(0);
animation:iconFloat 5s ease-in-out infinite;
}
@keyframes iconFloat{
0%,100%{transform:perspective(300px) translateZ(0) rotateY(0deg);}
50%{transform:perspective(300px) translateZ(10px) rotateY(8deg);}
}
.sec-icon svg{width:26px;height:26px;stroke:#fff;fill:none;stroke-width:1.8;stroke-linecap:round;stroke-linejoin:round;opacity:0.85;}
.sec-title{
font-family:‘Bebas Neue’,Impact,sans-serif;font-size:36px;
letter-spacing:4px;color:#fff;
text-shadow:0 0 20px rgba(255,255,255,0.2);
}
.overview{text-align:center;padding:80px 52px 0;position:relative;z-index:1;max-width:1320px;margin:0 auto;background:#000;}
.sec-tag{font-family:‘Share Tech Mono’,monospace;font-size:11px;letter-spacing:3px;color:#555;text-transform:uppercase;display:block;margin-bottom:20px;}
.overview h2{font-family:‘Bebas Neue’,Impact,sans-serif;font-size:clamp(40px,6vw,70px);letter-spacing:5px;color:#fff;margin-bottom:16px;text-shadow:0 0 30px rgba(255,255,255,0.2);}
.overview h2 span{color:transparent;-webkit-text-stroke:1px rgba(255,255,255,0.45);}
.overview p{font-size:17px;color:#666;max-width:540px;margin:0 auto;line-height:1.7;}

/* 3D CARDS */
.cards-3{display:grid;grid-template-columns:repeat(3,1fr);gap:18px;}
.cards-4{display:grid;grid-template-columns:repeat(4,1fr);gap:14px;}

.card{
background:#0d0d0d;
border:1px solid rgba(255,255,255,0.1);
padding:36px 30px;border-radius:22px;
position:relative;overflow:hidden;
transform:perspective(800px) translateZ(0) rotateX(0deg) rotateY(0deg);
transform-style:preserve-3d;
transition:transform 0.5s cubic-bezier(0.175,0.885,0.32,1.275), box-shadow 0.5s, border-color 0.5s, background 0.5s;
cursor:pointer;
box-shadow:0 4px 24px rgba(0,0,0,0.4),inset 0 0 20px rgba(255,255,255,0.02);
will-change:transform;
}
.card::before{
content:’’;position:absolute;top:0;left:0;right:0;height:1px;
background:linear-gradient(90deg,transparent,rgba(255,255,255,0.3),transparent);
opacity:0.25;transition:opacity 0.4s;
}
.card::after{
content:’’;
position:absolute;inset:0;border-radius:22px;
background:radial-gradient(circle at var(–mx,50%) var(–my,50%),rgba(255,255,255,0.04) 0%,transparent 60%);
opacity:0;transition:opacity 0.3s;
pointer-events:none;
}
.card:hover::after{opacity:1;}
.card:hover{
background:#111;
border-color:rgba(255,255,255,0.28);
box-shadow:0 20px 60px rgba(0,0,0,0.7),0 0 30px rgba(255,255,255,0.06),0 0 80px rgba(255,255,255,0.03),inset 0 0 30px rgba(255,255,255,0.03);
}
.card:hover::before{opacity:1;}

/* 3D card icon */
.card-icon{
width:54px;height:54px;background:#161616;
border:1px solid rgba(255,255,255,0.2);border-radius:15px;
display:flex;align-items:center;justify-content:center;
margin-bottom:22px;
box-shadow:0 0 14px rgba(255,255,255,0.1),0 0 30px rgba(255,255,255,0.04),inset 0 0 10px rgba(255,255,255,0.03);
transition:all 0.5s cubic-bezier(0.175,0.885,0.32,1.275);
transform:translateZ(20px);
}
.card-icon svg{width:24px;height:24px;stroke:#fff;fill:none;stroke-width:1.8;stroke-linecap:round;stroke-linejoin:round;opacity:0.8;transition:all 0.4s;}
.card:hover .card-icon{
border-color:rgba(255,255,255,0.5);
transform:translateZ(40px) scale(1.12) rotateY(-8deg);
box-shadow:0 0 24px rgba(255,255,255,0.25),0 0 60px rgba(255,255,255,0.1),inset 0 0 16px rgba(255,255,255,0.07);
}
.card:hover .card-icon svg{opacity:1;stroke-width:2;}
.card h3{
font-family:‘Bebas Neue’,Impact,sans-serif;font-size:20px;letter-spacing:2px;
color:#fff;margin-bottom:16px;
text-shadow:0 0 14px rgba(255,255,255,0.3);
transform:translateZ(10px);
transition:transform 0.5s;
}
.card:hover h3{transform:translateZ(25px);}
.card ul{list-style:none;display:flex;flex-direction:column;gap:10px;transform:translateZ(5px);transition:transform 0.5s;}
.card:hover ul{transform:translateZ(15px);}
.card ul li{display:flex;align-items:flex-start;gap:10px;font-size:15px;font-weight:400;color:rgba(200,200,200,0.7);line-height:1.4;}
.card ul li::before{content:”—”;color:rgba(255,255,255,0.2);flex-shrink:0;}

/* SCROLL ANIMATIONS */
.fade-up{opacity:0;transform:translateY(50px) rotateX(15deg);transition:opacity 0.8s ease,transform 0.8s ease;}
.fade-up.visible{opacity:1;transform:translateY(0) rotateX(0deg);}
.fade-up-delay-1{transition-delay:0.1s;}
.fade-up-delay-2{transition-delay:0.2s;}
.fade-up-delay-3{transition-delay:0.3s;}
@keyframes fadeUp{from{opacity:0;transform:translateY(30px)}to{opacity:1;transform:translateY(0)}}

.divider{position:relative;z-index:1;height:1px;background:linear-gradient(90deg,transparent,rgba(255,255,255,0.07),transparent);}

/* CTA */
.cta-sec{
position:relative;z-index:1;text-align:center;padding:100px 52px;
background:#050505;
border-top:1px solid rgba(255,255,255,0.07);border-bottom:1px solid rgba(255,255,255,0.07);
}
.cta-sec h2{
font-family:‘Bebas Neue’,Impact,sans-serif;font-size:clamp(36px,5vw,60px);
letter-spacing:5px;color:#fff;margin-bottom:16px;
text-shadow:0 0 30px rgba(255,255,255,0.35),0 0 80px rgba(255,255,255,0.12);
animation:titleFloat 6s ease-in-out infinite;
}
.cta-sec p{font-size:17px;color:#666;margin-bottom:48px;}

/* PRICING */
.pricing-wrap{position:relative;z-index:1;padding:100px 52px;max-width:960px;margin:0 auto;background:#000;}
.pricing-title{text-align:center;margin-bottom:56px;}
.pricing-title h2{font-family:‘Bebas Neue’,Impact,sans-serif;font-size:56px;letter-spacing:5px;color:#fff;text-shadow:0 0 30px rgba(255,255,255,0.2);}
.pricing-title h2 span{color:transparent;-webkit-text-stroke:1px rgba(255,255,255,0.4);}
.pricing-title p{color:#666;font-size:16px;margin-top:8px;}
.pricing-grid{display:grid;grid-template-columns:1fr 1fr;gap:18px;}
.price-card{
background:#0d0d0d;border:1px solid rgba(255,255,255,0.1);
padding:52px 44px;text-align:center;border-radius:26px;
position:relative;overflow:hidden;
transform:perspective(800px) translateZ(0);
transition:all 0.5s cubic-bezier(0.175,0.885,0.32,1.275);
}
.price-card.premium{background:#0f0f0f;border-color:rgba(255,255,255,0.25);box-shadow:0 0 40px rgba(255,255,255,0.04);}
.price-card.premium::before{content:’’;position:absolute;top:0;left:0;right:0;height:1px;background:linear-gradient(90deg,transparent,rgba(255,255,255,0.55),transparent);box-shadow:0 0 12px rgba(255,255,255,0.3);}
.price-card:hover{transform:perspective(800px) translateZ(20px) rotateX(-2deg);box-shadow:0 30px 80px rgba(0,0,0,0.7),0 0 30px rgba(255,255,255,0.08);}
.price-badge{display:flex;justify-content:center;margin-bottom:20px;}
.price-name{font-family:‘Bebas Neue’,Impact,sans-serif;font-size:26px;letter-spacing:3px;color:#fff;margin-bottom:36px;text-shadow:0 0 12px rgba(255,255,255,0.2);}
.price-feats{list-style:none;text-align:left;display:flex;flex-direction:column;gap:14px;margin-bottom:44px;}
.price-feats li{display:flex;align-items:center;gap:12px;font-size:16px;color:#888;}
.price-feats li::before{content:“✓”;color:#fff;font-weight:700;font-size:14px;}
.btn-free{font-family:‘Rajdhani’,Arial,sans-serif;font-size:13px;font-weight:700;letter-spacing:2px;text-transform:uppercase;padding:15px 32px;background:transparent;color:#fff;border:1px solid rgba(255,255,255,0.25);border-radius:30px;cursor:pointer;text-decoration:none;display:block;transition:all 0.3s;}
.btn-free:hover{background:rgba(255,255,255,0.05);box-shadow:0 0 14px rgba(255,255,255,0.12);transform:perspective(400px) translateZ(8px);}
.btn-prem{font-family:‘Rajdhani’,Arial,sans-serif;font-size:13px;font-weight:700;letter-spacing:2px;text-transform:uppercase;padding:15px 32px;background:#fff;color:#000;border:none;border-radius:30px;cursor:pointer;text-decoration:none;display:block;transition:all 0.3s;box-shadow:0 0 14px rgba(255,255,255,0.2);}
.btn-prem:hover{transform:perspective(400px) translateZ(12px) translateY(-2px);box-shadow:0 0 30px rgba(255,255,255,0.4),0 0 80px rgba(255,255,255,0.15);}

/* SUPPORT */
.support-wrap{position:relative;z-index:1;text-align:center;padding:100px 52px;max-width:800px;margin:0 auto;background:#000;}
.support-card{
background:#0d0d0d;border:1px solid rgba(255,255,255,0.15);padding:64px;
text-align:center;position:relative;border-radius:26px;
box-shadow:0 0 40px rgba(255,255,255,0.03);
transform:perspective(800px) translateZ(0);
transition:transform 0.5s,box-shadow 0.5s;
}
.support-card:hover{transform:perspective(800px) translateZ(16px);box-shadow:0 0 40px rgba(255,255,255,0.08),0 30px 80px rgba(0,0,0,0.6);}
.support-card::before{content:’’;position:absolute;top:0;left:0;right:0;height:1px;background:linear-gradient(90deg,transparent,rgba(255,255,255,0.35),transparent);box-shadow:0 0 10px rgba(255,255,255,0.2);border-radius:26px 26px 0 0;}
.support-icon{
width:72px;height:72px;background:#1a1a1a;border:1px solid rgba(255,255,255,0.2);border-radius:50%;
display:flex;align-items:center;justify-content:center;margin:0 auto 24px;
box-shadow:0 0 20px rgba(255,255,255,0.08);
animation:iconFloat 5s ease-in-out infinite;
}
.support-icon svg{width:32px;height:32px;stroke:#fff;fill:none;stroke-width:1.8;stroke-linecap:round;stroke-linejoin:round;opacity:0.85;}
.support-card h3{font-family:‘Bebas Neue’,Impact,sans-serif;font-size:26px;letter-spacing:3px;color:#fff;margin-bottom:12px;text-shadow:0 0 14px rgba(255,255,255,0.2);}
.support-card p{font-size:16px;color:#666;line-height:1.7;margin-bottom:36px;}

/* FOOTER */
footer{position:relative;z-index:1;padding:64px 52px 40px;border-top:1px solid rgba(255,255,255,0.07);background:#030303;}
.foot-grid{display:grid;grid-template-columns:2fr 1fr 1fr;gap:52px;margin-bottom:52px;}
.foot-brand p{font-size:15px;color:#555;line-height:1.7;margin-top:16px;max-width:280px;}
.foot-col h4{font-family:‘Share Tech Mono’,monospace;font-size:11px;letter-spacing:3px;color:#555;text-transform:uppercase;margin-bottom:24px;}
.foot-col ul{list-style:none;display:flex;flex-direction:column;gap:12px;}
.foot-col a{font-size:15px;color:#444;text-decoration:none;transition:all 0.3s;}
.foot-col a:hover{color:#fff;text-shadow:0 0 8px rgba(255,255,255,0.4);}
.foot-bottom{display:flex;justify-content:space-between;align-items:center;padding-top:32px;border-top:1px solid rgba(255,255,255,0.07);font-family:‘Share Tech Mono’,monospace;font-size:11px;letter-spacing:1px;color:#444;}

@media(max-width:900px){
nav{padding:16px 24px;}.nav-links{display:none;}
section{padding:60px 24px;}
.cards-3,.cards-4{grid-template-columns:1fr 1fr;}
.pricing-grid{grid-template-columns:1fr;}
.foot-grid{grid-template-columns:1fr;}
.stats{flex-wrap:wrap;}
.stat{border-right:none;border-bottom:1px solid rgba(255,255,255,0.07);padding:20px;}
}
@media(max-width:600px){.cards-3,.cards-4{grid-template-columns:1fr;}}
</style>

</head>
<body>

<canvas id="particles"></canvas>

<!-- SVG DEFS -->

<svg style="display:none" xmlns="http://www.w3.org/2000/svg"><defs>
<symbol id="ico-chat" viewBox="0 0 24 24"><path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2z"/></symbol>
<symbol id="ico-image" viewBox="0 0 24 24"><rect x="3" y="3" width="18" height="18" rx="2"/><circle cx="8.5" cy="8.5" r="1.5"/><polyline points="21 15 16 10 5 21"/></symbol>
<symbol id="ico-mic" viewBox="0 0 24 24"><path d="M12 1a3 3 0 0 0-3 3v8a3 3 0 0 0 6 0V4a3 3 0 0 0-3-3z"/><path d="M19 10v2a7 7 0 0 1-14 0v-2"/><line x1="12" y1="19" x2="12" y2="23"/><line x1="8" y1="23" x2="16" y2="23"/></symbol>
<symbol id="ico-shield" viewBox="0 0 24 24"><path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/></symbol>
<symbol id="ico-zap" viewBox="0 0 24 24"><polygon points="13 2 3 14 12 14 11 22 21 10 12 10 13 2"/></symbol>
<symbol id="ico-settings" viewBox="0 0 24 24"><circle cx="12" cy="12" r="3"/><path d="M19.4 15a1.65 1.65 0 0 0 .33 1.82l.06.06a2 2 0 0 1-2.83 2.83l-.06-.06a1.65 1.65 0 0 0-1.82-.33 1.65 1.65 0 0 0-1 1.51V21a2 2 0 0 1-4 0v-.09A1.65 1.65 0 0 0 9 19.4a1.65 1.65 0 0 0-1.82.33l-.06-.06a2 2 0 0 1-2.83-2.83l.06-.06A1.65 1.65 0 0 0 4.68 15a1.65 1.65 0 0 0-1.51-1H3a2 2 0 0 1 0-4h.09A1.65 1.65 0 0 0 4.6 9a1.65 1.65 0 0 0-.33-1.82l-.06-.06a2 2 0 0 1 2.83-2.83l.06.06A1.65 1.65 0 0 0 9 4.68a1.65 1.65 0 0 0 1-1.51V3a2 2 0 0 1 4 0v.09a1.65 1.65 0 0 0 1 1.51 1.65 1.65 0 0 0 1.82-.33l.06-.06a2 2 0 0 1 2.83 2.83l-.06.06A1.65 1.65 0 0 0 19.4 9a1.65 1.65 0 0 0 1.51 1H21a2 2 0 0 1 0 4h-.09a1.65 1.65 0 0 0-1.51 1z"/></symbol>
<symbol id="ico-file" viewBox="0 0 24 24"><path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"/><polyline points="14 2 14 8 20 8"/><line x1="16" y1="13" x2="8" y2="13"/><line x1="16" y1="17" x2="8" y2="17"/></symbol>
<symbol id="ico-user-plus" viewBox="0 0 24 24"><path d="M16 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2"/><circle cx="8.5" cy="7" r="4"/><line x1="20" y1="8" x2="20" y2="14"/><line x1="23" y1="11" x2="17" y2="11"/></symbol>
<symbol id="ico-ticket" viewBox="0 0 24 24"><path d="M2 9a3 3 0 0 1 0 6v2a2 2 0 0 0 2 2h16a2 2 0 0 0 2-2v-2a3 3 0 0 1 0-6V7a2 2 0 0 0-2-2H4a2 2 0 0 0-2 2v2z"/></symbol>
<symbol id="ico-calendar" viewBox="0 0 24 24"><rect x="3" y="4" width="18" height="18" rx="2"/><line x1="16" y1="2" x2="16" y2="6"/><line x1="8" y1="2" x2="8" y2="6"/><line x1="3" y1="10" x2="21" y2="10"/></symbol>
<symbol id="ico-poll" viewBox="0 0 24 24"><line x1="18" y1="20" x2="18" y2="10"/><line x1="12" y1="20" x2="12" y2="4"/><line x1="6" y1="20" x2="6" y2="14"/></symbol>
<symbol id="ico-clock" viewBox="0 0 24 24"><circle cx="12" cy="12" r="10"/><polyline points="12 6 12 12 16 14"/></symbol>
<symbol id="ico-bell" viewBox="0 0 24 24"><path d="M18 8A6 6 0 0 0 6 8c0 7-3 9-3 9h18s-3-2-3-9"/><path d="M13.73 21a2 2 0 0 1-3.46 0"/></symbol>
<symbol id="ico-trending" viewBox="0 0 24 24"><polyline points="23 6 13.5 15.5 8.5 10.5 1 18"/><polyline points="17 6 23 6 23 12"/></symbol>
<symbol id="ico-photo" viewBox="0 0 24 24"><rect x="3" y="3" width="18" height="18" rx="2"/><circle cx="8.5" cy="8.5" r="1.5"/><polyline points="21 15 16 10 5 21"/></symbol>
<symbol id="ico-dice" viewBox="0 0 24 24"><rect x="2" y="2" width="20" height="20" rx="3"/><circle cx="8" cy="8" r="1.2" fill="white" stroke="none"/><circle cx="16" cy="8" r="1.2" fill="white" stroke="none"/><circle cx="8" cy="16" r="1.2" fill="white" stroke="none"/><circle cx="16" cy="16" r="1.2" fill="white" stroke="none"/><circle cx="12" cy="12" r="1.2" fill="white" stroke="none"/></symbol>
<symbol id="ico-smile" viewBox="0 0 24 24"><circle cx="12" cy="12" r="10"/><path d="M8 13s1.5 2 4 2 4-2 4-2"/><line x1="9" y1="9" x2="9.01" y2="9"/><line x1="15" y1="9" x2="15.01" y2="9"/></symbol>
<symbol id="ico-award" viewBox="0 0 24 24"><circle cx="12" cy="8" r="6"/><path d="M15.477 12.89L17 22l-5-3-5 3 1.523-9.11"/></symbol>
<symbol id="ico-activity" viewBox="0 0 24 24"><polyline points="22 12 18 12 15 21 9 3 6 12 2 12"/></symbol>
<symbol id="ico-terminal" viewBox="0 0 24 24"><polyline points="4 17 10 11 4 5"/><line x1="12" y1="19" x2="20" y2="19"/></symbol>
<symbol id="ico-globe" viewBox="0 0 24 24"><circle cx="12" cy="12" r="10"/><line x1="2" y1="12" x2="22" y2="12"/><path d="M12 2a15.3 15.3 0 0 1 4 10 15.3 15.3 0 0 1-4 10 15.3 15.3 0 0 1-4-10 15.3 15.3 0 0 1 4-10z"/></symbol>
<symbol id="ico-robot" viewBox="0 0 24 24"><rect x="3" y="11" width="18" height="10" rx="2"/><path d="M12 11V7"/><circle cx="12" cy="5" r="2"/><line x1="8" y1="15" x2="8" y2="15" stroke-width="3"/><line x1="16" y1="15" x2="16" y2="15" stroke-width="3"/><line x1="8" y1="19" x2="16" y2="19"/></symbol>
<symbol id="ico-sword" viewBox="0 0 24 24"><polyline points="14.5 17.5 3 6 3 3 6 3 17.5 14.5"/><line x1="13" y1="19" x2="19" y2="13"/><line x1="16" y1="16" x2="20" y2="20"/><line x1="19" y1="21" x2="21" y2="19"/></symbol>
<symbol id="ico-people" viewBox="0 0 24 24"><path d="M17 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2"/><circle cx="9" cy="7" r="4"/><path d="M23 21v-2a4 4 0 0 0-3-3.87"/><path d="M16 3.13a4 4 0 0 1 0 7.75"/></symbol>
<symbol id="ico-server" viewBox="0 0 24 24"><rect x="2" y="2" width="20" height="8" rx="2"/><rect x="2" y="14" width="20" height="8" rx="2"/><line x1="6" y1="6" x2="6.01" y2="6"/><line x1="6" y1="18" x2="6.01" y2="18"/></symbol>
<symbol id="ico-monitor" viewBox="0 0 24 24"><rect x="2" y="3" width="20" height="14" rx="2"/><line x1="8" y1="21" x2="16" y2="21"/><line x1="12" y1="17" x2="12" y2="21"/></symbol>
<symbol id="ico-gamepad" viewBox="0 0 24 24"><line x1="6" y1="12" x2="10" y2="12"/><line x1="8" y1="10" x2="8" y2="14"/><line x1="15" y1="13" x2="15.01" y2="13" stroke-width="3"/><line x1="18" y1="11" x2="18.01" y2="11" stroke-width="3"/><path d="M6 20h12a2 2 0 0 0 2-2V8a2 2 0 0 0-2-2H6a2 2 0 0 0-2 2v10a2 2 0 0 0 2 2z"/></symbol>
<symbol id="ico-headphones" viewBox="0 0 24 24"><path d="M3 18v-6a9 9 0 0 1 18 0v6"/><path d="M21 19a2 2 0 0 1-2 2h-1a2 2 0 0 1-2-2v-3a2 2 0 0 1 2-2h3z"/><path d="M3 19a2 2 0 0 0 2 2h1a2 2 0 0 0 2-2v-3a2 2 0 0 0-2-2H3z"/></symbol>
<symbol id="ico-translate" viewBox="0 0 24 24"><path d="M5 8l6 6"/><path d="M4 14l6-6 2-3"/><path d="M2 5h12"/><path d="M7 2h1"/><path d="M22 22l-5-10-5 10"/><path d="M14 18h6"/></symbol>
</defs></svg>

<nav>
  <a href="#" class="logo">
    <div class="logo-img-wrap">
      <img src="data:image/jpeg;base64,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" alt="Dark Vortex" class="logo-img">
    </div>
    <span class="logo-text">Dark Vortex</span>
  </a>
  <ul class="nav-links">
    <li><a href="#features">Features</a></li>
    <li><a href="#commands">Commands</a></li>
    <li><a href="#premium">Premium</a></li>
    <li><a href="#support">Support</a></li>
  </ul>
  <a href="#" class="nav-cta">Add to Discord</a>
</nav>

<div class="hero">
  <div class="vortex-bg">
    <div class="vortex-ring"></div><div class="vortex-ring"></div>
    <div class="vortex-ring"></div><div class="vortex-ring"></div><div class="vortex-ring"></div>
  </div>
  <div class="hero-badge">// AI POWERED //</div>
  <div class="pfp-wrap">
    <div class="pfp-ring3"></div>
    <div class="pfp-ring1"></div>
    <div class="pfp-ring2"></div>
    <img src="data:image/jpeg;base64,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" alt="Dark Vortex" class="hero-pfp">
    <div class="pfp-shadow"></div>
  </div>
  <h1><span class="l1">Dark Vortex</span><span class="l2">Consumes All</span></h1>
  <p class="hero-sub">The Discord bot that dwells in darkness. Advanced moderation, AI intelligence, and total community control — pulled from the void.</p>
  <div class="hero-btns">
    <a href="#" class="btn-primary">&#8594; Summon Dark Vortex</a>
    <a href="#" class="btn-outline">&#8853; Enter the Void</a>
  </div>
</div>

<div class="stats">
  <div class="stat fade-up"><div class="stat-num">500+</div><div class="stat-label">Active Servers</div></div>
  <div class="stat fade-up fade-up-delay-1"><div class="stat-num">50K+</div><div class="stat-label">Users Served</div></div>
  <div class="stat fade-up fade-up-delay-2"><div class="stat-num">99.9%</div><div class="stat-label">Uptime</div></div>
</div>

<div class="overview fade-up">
  <span class="sec-tag">// Features Overview</span>
  <h2>Powerful Tools for <span>Modern Communities</span></h2>
  <p>Explore the complete arsenal that makes Dark Vortex the ultimate all-in-one Discord solution.</p>
</div>

<section id="features">
  <div class="section-head fade-up"><div class="sec-icon"><svg><use href="#ico-robot"/></svg></div><h2 class="sec-title">AI Features</h2></div>
  <div class="cards-3">
    <div class="card fade-up"><div class="card-icon"><svg><use href="#ico-chat"/></svg></div><h3>AI Chat</h3><ul><li>Natural language conversations</li><li>Context-aware responses</li><li>Multi-turn memory</li></ul></div>
    <div class="card fade-up fade-up-delay-1"><div class="card-icon"><svg><use href="#ico-image"/></svg></div><h3>Image Generation</h3><ul><li>AI-powered image creation</li><li>Custom style options</li><li>Dark art presets</li></ul></div>
    <div class="card fade-up fade-up-delay-2"><div class="card-icon"><svg><use href="#ico-mic"/></svg></div><h3>Voice AI</h3><ul><li>Voice message responses</li><li>Natural voice synthesis</li><li>Multiple voice styles</li></ul></div>
  </div>
</section>
<div class="divider"></div>

<section>
  <div class="section-head fade-up"><div class="sec-icon"><svg><use href="#ico-shield"/></svg></div><h2 class="sec-title">Moderation Features</h2></div>
  <div class="cards-4">
    <div class="card fade-up"><div class="card-icon"><svg><use href="#ico-sword"/></svg></div><h3>Advanced Moderation</h3><ul><li>Ban, kick &amp; timeout</li><li>Warning system</li></ul></div>
    <div class="card fade-up fade-up-delay-1"><div class="card-icon"><svg><use href="#ico-zap"/></svg></div><h3>Anti-Spam &amp; Security</h3><ul><li>Protect against raids</li><li>Configurable security</li></ul></div>
    <div class="card fade-up fade-up-delay-2"><div class="card-icon"><svg><use href="#ico-settings"/></svg></div><h3>Auto-Moderation</h3><ul><li>Automatic filtering</li><li>Customizable rules</li></ul></div>
    <div class="card fade-up fade-up-delay-3"><div class="card-icon"><svg><use href="#ico-file"/></svg></div><h3>Logging System</h3><ul><li>Detailed mod logs</li><li>User activity tracking</li></ul></div>
  </div>
</section>
<div class="divider"></div>

<section id="commands">
  <div class="section-head fade-up"><div class="sec-icon"><svg><use href="#ico-server"/></svg></div><h2 class="sec-title">Utility Features</h2></div>
  <div class="cards-4">
    <div class="card fade-up"><div class="card-icon"><svg><use href="#ico-user-plus"/></svg></div><h3>Auto-Role</h3><ul><li>Automatic role assignment</li><li>Multiple role configs</li></ul></div>
    <div class="card fade-up fade-up-delay-1"><div class="card-icon"><svg><use href="#ico-ticket"/></svg></div><h3>Support Tickets</h3><ul><li>Private support channels</li><li>Anonymous reporting</li></ul></div>
    <div class="card fade-up fade-up-delay-2"><div class="card-icon"><svg><use href="#ico-calendar"/></svg></div><h3>Event System</h3><ul><li>Event scheduling</li><li>Automated reminders</li></ul></div>
    <div class="card fade-up fade-up-delay-3"><div class="card-icon"><svg><use href="#ico-poll"/></svg></div><h3>Polls &amp; Voting</h3><ul><li>Interactive poll creation</li><li>Real-time vote tracking</li></ul></div>
  </div>
</section>
<div class="divider"></div>

<section>
  <div class="section-head fade-up"><div class="sec-icon"><svg><use href="#ico-monitor"/></svg></div><h2 class="sec-title">Server Management</h2></div>
  <div class="cards-3">
    <div class="card fade-up"><div class="card-icon"><svg><use href="#ico-clock"/></svg></div><h3>Temporary Channels</h3><ul><li>Time-limited text channels</li><li>Auto-deletion after expiry</li><li>Custom channel settings</li></ul></div>
    <div class="card fade-up fade-up-delay-1"><div class="card-icon"><svg><use href="#ico-bell"/></svg></div><h3>Reminder System</h3><ul><li>Set custom reminders</li><li>Flexible time formats</li><li>Recurring reminders</li></ul></div>
    <div class="card fade-up fade-up-delay-2"><div class="card-icon"><svg><use href="#ico-trending"/></svg></div><h3>Server Statistics</h3><ul><li>Detailed server information</li><li>Member activity tracking</li><li>Growth analytics</li></ul></div>
  </div>
</section>
<div class="divider"></div>

<section>
  <div class="section-head fade-up"><div class="sec-icon"><svg><use href="#ico-gamepad"/></svg></div><h2 class="sec-title">Entertainment</h2></div>
  <div class="cards-3">
    <div class="card fade-up"><div class="card-icon"><svg><use href="#ico-photo"/></svg></div><h3>Media Commands</h3><ul><li>Random meme generator</li><li>Cat pictures with fun facts</li><li>Anime image gallery</li></ul></div>
    <div class="card fade-up fade-up-delay-1"><div class="card-icon"><svg><use href="#ico-dice"/></svg></div><h3>Fun Games</h3><ul><li>Dice rolling with custom sides</li><li>Interactive riddles</li><li>Playful hacking simulation</li></ul></div>
    <div class="card fade-up fade-up-delay-2"><div class="card-icon"><svg><use href="#ico-smile"/></svg></div><h3>Fun Interactions</h3><ul><li>Dad jokes generator</li><li>Dark humor mode</li><li>Friendly roasts &amp; compliments</li></ul></div>
  </div>
</section>
<div class="divider"></div>

<section>
  <div class="section-head fade-up"><div class="sec-icon"><svg><use href="#ico-people"/></svg></div><h2 class="sec-title">Community Features</h2></div>
  <div class="cards-3">
    <div class="card fade-up"><div class="card-icon"><svg><use href="#ico-award"/></svg></div><h3>Points System</h3><ul><li>Activity-based rewards</li><li>Custom point allocation</li><li>Leaderboards</li></ul></div>
    <div class="card fade-up fade-up-delay-1"><div class="card-icon"><svg><use href="#ico-activity"/></svg></div><h3>Analytics</h3><ul><li>Server activity insights</li><li>Engagement tracking</li><li>Member growth reports</li></ul></div>
    <div class="card fade-up fade-up-delay-2"><div class="card-icon"><svg><use href="#ico-terminal"/></svg></div><h3>Custom Commands</h3><ul><li>Create custom responses</li><li>Personalized triggers</li><li>Variable support</li></ul></div>
  </div>
</section>
<div class="divider"></div>

<section>
  <div class="section-head fade-up"><div class="sec-icon"><svg><use href="#ico-globe"/></svg></div><h2 class="sec-title">Translation Features</h2></div>
  <div style="max-width:380px;">
    <div class="card fade-up"><div class="card-icon"><svg><use href="#ico-translate"/></svg></div><h3>Multi-Language Support</h3><ul><li>Translate text between languages</li><li>Support for multiple language codes</li><li>Auto-detect source language</li></ul></div>
  </div>
</section>

<div class="cta-sec fade-up">
  <h2>Ready to Enter the Void?</h2>
  <p>Invite Dark Vortex and unleash absolute order upon your server.</p>
  <a href="#" class="btn-primary">&#8594; Invite Dark Vortex Now</a>
</div>

<div class="pricing-wrap" id="premium">
  <div class="pricing-title fade-up">
    <span class="sec-tag">// Choose Your Power</span>
    <h2>Subscription <span>Plans</span></h2>
    <p>Choose the darkness that suits your realm</p>
  </div>
  <div class="pricing-grid">
    <div class="price-card fade-up">
      <div class="price-badge"><svg width="48" height="48" viewBox="0 0 24 24" fill="none" stroke="rgba(255,255,255,0.55)" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><polygon points="12 2 15.09 8.26 22 9.27 17 14.14 18.18 21.02 12 17.77 5.82 21.02 7 14.14 2 9.27 8.91 8.26 12 2"/></svg></div>
      <div class="price-name">Dark Vortex Free</div>
      <ul class="price-feats"><li>Access to all basic features</li><li>Moderation commands</li><li>Basic AI features</li><li>Entertainment commands</li><li>Server management tools</li></ul>
      <a href="#" class="btn-free">+ Add for Free</a>
    </div>
    <div class="price-card premium fade-up fade-up-delay-1">
      <div class="price-badge"><svg width="48" height="48" viewBox="0 0 24 24" fill="none" stroke="rgba(255,255,255,0.9)" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><path d="M2 20h20M5 20l-1-8 5 4 3-8 3 8 5-4-1 8"/></svg></div>
      <div class="price-name">Dark Vortex Premium</div>
      <ul class="price-feats"><li>All Free features included</li><li>Advanced AI features</li><li>Unlimited image generation</li><li>Voice AI responses</li><li>Priority void support</li></ul>
      <a href="#" class="btn-prem">Unlock Premium Power</a>
    </div>
  </div>
</div>

<div class="support-wrap" id="support">
  <span class="sec-tag">// We're Here</span>
  <h2 style="font-family:'Bebas Neue',Impact,sans-serif;font-size:56px;letter-spacing:5px;color:#fff;margin-bottom:12px;text-shadow:0 0 30px rgba(255,255,255,0.2);">Need <span style="color:transparent;-webkit-text-stroke:1px rgba(255,255,255,0.4);">Support?</span></h2>
  <p style="font-size:17px;color:#666;margin-bottom:0;">The Dark Vortex council awaits.</p>
  <div class="support-card fade-up" style="margin-top:56px;">
    <div class="support-icon"><svg><use href="#ico-headphones"/></svg></div>
    <h3>Join the Dark Server</h3>
    <p>The fastest way to get help. Join our community, open a ticket, or speak directly with our developers.</p>
    <a href="#" class="btn-primary" style="display:inline-flex;">&#8594; Join Support Server</a>
  </div>
</div>

<footer>
  <div class="foot-grid">
    <div class="foot-brand">
      <a href="#" class="logo">
        <div class="logo-img-wrap" style="animation-duration:12s;">
          <img src="data:image/jpeg;base64,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" alt="Dark Vortex" class="logo-img">
        </div>
        <span class="logo-text">Dark Vortex</span>
      </a>
      <p>The next-generation AI companion for Discord communities. Moderation, entertainment, and utility — consumed by darkness.</p>
    </div>
    <div class="foot-col">
      <h4>Product</h4>
      <ul><li><a href="#">Features</a></li><li><a href="#">Premium</a></li><li><a href="#">Commands</a></li></ul>
    </div>
    <div class="foot-col">
      <h4>Legal</h4>
      <ul><li><a href="#">Privacy Policy</a></li><li><a href="#">Terms of Service</a></li><li><a href="#">Cookie Policy</a></li></ul>
    </div>
  </div>
  <div class="foot-bottom">
    <span>&copy; 2026 DARK VORTEX. ALL RIGHTS RESERVED.</span>
    <span>MADE WITH &hearts; BY THE DARK VORTEX TEAM</span>
  </div>
</footer>

<script>
// === PARTICLE SYSTEM ===
const canvas = document.getElementById('particles');
const ctx = canvas.getContext('2d');
let W, H, particles = [];

function resize() {
  W = canvas.width = window.innerWidth;
  H = canvas.height = window.innerHeight;
}
resize();
window.addEventListener('resize', resize);

class Particle {
  constructor() { this.reset(); }
  reset() {
    this.x = Math.random() * W;
    this.y = Math.random() * H;
    this.r = Math.random() * 1.2 + 0.3;
    this.vx = (Math.random() - 0.5) * 0.3;
    this.vy = (Math.random() - 0.5) * 0.3;
    this.alpha = Math.random() * 0.4 + 0.05;
    this.life = Math.random() * 200 + 100;
    this.age = 0;
  }
  update() {
    this.x += this.vx; this.y += this.vy; this.age++;
    if (this.age > this.life) this.reset();
  }
  draw() {
    const fade = this.age < 30 ? this.age/30 : this.age > this.life-30 ? (this.life-this.age)/30 : 1;
    ctx.globalAlpha = this.alpha * fade;
    ctx.beginPath();
    ctx.arc(this.x, this.y, this.r, 0, Math.PI * 2);
    ctx.fillStyle = '#fff';
    ctx.fill();
  }
}

for (let i = 0; i < 120; i++) particles.push(new Particle());

function animateParticles() {
  ctx.clearRect(0, 0, W, H);
  particles.forEach(p => { p.update(); p.draw(); });
  ctx.globalAlpha = 1;
  requestAnimationFrame(animateParticles);
}
animateParticles();

// === 3D CARD TILT on mouse ===
document.querySelectorAll('.card').forEach(card => {
  card.addEventListener('mousemove', e => {
    const r = card.getBoundingClientRect();
    const x = e.clientX - r.left;
    const y = e.clientY - r.top;
    const cx = r.width / 2, cy = r.height / 2;
    const rotY = ((x - cx) / cx) * 12;
    const rotX = -((y - cy) / cy) * 8;
    card.style.transform = `perspective(800px) rotateX(${rotX}deg) rotateY(${rotY}deg) translateZ(10px)`;
    // mouse highlight
    const pct = (x / r.width * 100).toFixed(1);
    const pct2 = (y / r.height * 100).toFixed(1);
    card.style.setProperty('--mx', pct + '%');
    card.style.setProperty('--my', pct2 + '%');
  });
  card.addEventListener('mouseleave', () => {
    card.style.transform = 'perspective(800px) rotateX(0deg) rotateY(0deg) translateZ(0)';
  });
});

// === SCROLL REVEAL ===
const obs = new IntersectionObserver(entries => {
  entries.forEach(e => {
    if (e.isIntersecting) { e.target.classList.add('visible'); obs.unobserve(e.target); }
  });
}, { threshold: 0.08, rootMargin: '0px 0px -50px 0px' });
document.querySelectorAll('.fade-up').forEach(el => obs.observe(el));

// === NAV logo 3D follow mouse ===
const logoWrap = document.querySelector('.logo-img-wrap');
document.addEventListener('mousemove', e => {
  const cx = window.innerWidth / 2;
  const cy = 40;
  const dx = (e.clientX - cx) / cx * 10;
  const dy = (e.clientY - cy) / 200 * 6;
  if(logoWrap) logoWrap.style.transform = `rotateY(${dx}deg) rotateX(${-dy}deg)`;
});
</script>

</body>
</html>

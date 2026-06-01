import { useState, useEffect, useRef } from "react";

const NAV_LINKS = ["Home","About","Services","Plans","Trainers","Transformations","Gallery","Reviews","Contact"];

const SERVICES = [
  { icon: "🏋️", title: "Personal Training", desc: "One-on-one sessions tailored to your goals with expert guidance and accountability." },
  { icon: "🔥", title: "Weight Loss", desc: "Science-backed programs combining cardio, strength, and nutrition for real results." },
  { icon: "💪", title: "Muscle Building", desc: "Progressive overload programming designed to maximize hypertrophy and strength gains." },
  { icon: "⚡", title: "Functional Training", desc: "Movement patterns that improve real-world performance, mobility, and injury prevention." },
  { icon: "👥", title: "Group Classes", desc: "High-energy group sessions — HIIT, Zumba, Yoga, and more. Community drives motivation." },
  { icon: "🥗", title: "Nutrition Coaching", desc: "Custom meal plans and dietary guidance to fuel your training and accelerate transformation." },
];

const PLANS = [
  {
    name: "Monthly",
    price: "₹1,499",
    period: "/month",
    features: ["Full gym access","Locker facility","Basic fitness assessment","1 free PT session","Group classes"],
    popular: false,
    color: "#39FF14",
  },
  {
    name: "Quarterly",
    price: "₹3,999",
    period: "/3 months",
    features: ["Everything in Monthly","2 PT sessions/month","Nutrition consultation","Progress tracking","Priority booking","Body composition analysis"],
    popular: true,
    color: "#39FF14",
  },
  {
    name: "Annual",
    price: "₹12,999",
    period: "/year",
    features: ["Everything in Quarterly","Unlimited PT sessions","Custom meal plan","24/7 access","Guest passes (4/month)","Free merchandise","VIP lounge access"],
    popular: false,
    color: "#39FF14",
  },
];

const TRAINERS = [
  { name: "Surjeet Kumar", role: "Head Trainer & Founder", exp: "10+ Years", cert: "ACSM Certified", specialty: "Strength & Conditioning", emoji: "👨‍🦱" },
  { name: "Karamjit Singh", role: "Nutrition & Weight Loss", exp: "7 Years", cert: "ISSA Nutrition Coach", specialty: "Body Transformation", emoji: "👨‍💼" },
  { name: "Priya Sharma", role: "Group Fitness & Yoga", exp: "5 Years", cert: "ACE Certified", specialty: "Functional & Yoga", emoji: "👩‍🦰" },
];

const REVIEWS = [
  { name: "Deepak Soni", rating: 5, text: "Budget friendly but gives luxurious look. All equipments are there! Best decision I made for my fitness journey.", date: "2 days ago" },
  { name: "Rattanjot Singh", rating: 5, text: "Everything's good! The trainers are highly professional and the atmosphere keeps you motivated every single day.", date: "2 days ago" },
  { name: "Shubhneet Goyal", rating: 5, text: "One of the best gyms in the area. The environment is very motivating, equipment is well maintained, and trainers are supportive and knowledgeable.", date: "2 days ago" },
  { name: "Fitness Enthusiast", rating: 5, text: "Clean space, good crowd, and positive vibes every day. Perfect place for anyone serious about fitness and health. Highly recommended!", date: "1 week ago" },
];

const TRANSFORMATIONS = [
  { name: "Rahul M.", loss: "-18 kg", time: "4 months", before: "95kg", after: "77kg" },
  { name: "Simran K.", loss: "-12 kg", time: "3 months", before: "72kg", after: "60kg" },
  { name: "Vikram S.", gain: "+8 kg muscle", time: "5 months", before: "65kg", after: "73kg" },
  { name: "Neha P.", loss: "-15 kg", time: "4 months", before: "80kg", after: "65kg" },
];

const GALLERY_ITEMS = [
  { label: "Free Weights Zone", emoji: "🏋️", bg: "#0a0a0a", desc: "Olympic bars, dumbbells up to 50kg, premium benches" },
  { label: "Cardio Floor", emoji: "🏃", bg: "#0d0d0d", desc: "Treadmills, bikes, rowing machines, ellipticals" },
  { label: "Functional Zone", emoji: "⚡", bg: "#0a0a0a", desc: "Battle ropes, TRX, kettlebells, sled tracks" },
  { label: "Group Studio", emoji: "🎵", bg: "#0d0d0d", desc: "450 sq ft mirrored studio with sound system" },
  { label: "Nutrition Bar", emoji: "🥤", bg: "#0a0a0a", desc: "Post-workout shakes, protein supplements" },
  { label: "Locker Room", emoji: "🚿", bg: "#0d0d0d", desc: "Premium lockers, showers, changing area" },
];

export default function SKTFitnessWorld() {
  const [activeNav, setActiveNav] = useState("Home");
  const [menuOpen, setMenuOpen] = useState(false);
  const [bmi, setBmi] = useState(null);
  const [height, setHeight] = useState(170);
  const [weight, setWeight] = useState(70);
  const [age, setAge] = useState(25);
  const [scrollY, setScrollY] = useState(0);
  const [visibleSections, setVisibleSections] = useState(new Set());
  const [reviewIdx, setReviewIdx] = useState(0);
  const [formData, setFormData] = useState({ name: "", phone: "", email: "", message: "" });
  const [formSent, setFormSent] = useState(false);
  const sectionRefs = useRef({});

  useEffect(() => {
    const onScroll = () => setScrollY(window.scrollY);
    window.addEventListener("scroll", onScroll);
    return () => window.removeEventListener("scroll", onScroll);
  }, []);

  useEffect(() => {
    const observer = new IntersectionObserver(
      (entries) => {
        entries.forEach((e) => {
          if (e.isIntersecting) setVisibleSections((prev) => new Set([...prev, e.target.id]));
        });
      },
      { threshold: 0.1 }
    );
    Object.values(sectionRefs.current).forEach((el) => el && observer.observe(el));
    return () => observer.disconnect();
  }, []);

  useEffect(() => {
    const timer = setInterval(() => setReviewIdx((i) => (i + 1) % REVIEWS.length), 4000);
    return () => clearInterval(timer);
  }, []);

  const calcBMI = () => {
    const h = height / 100;
    const result = (weight / (h * h)).toFixed(1);
    setBmi(result);
  };

  const bmiCategory = (b) => {
    if (b < 18.5) return { label: "Underweight", color: "#3B82F6" };
    if (b < 25) return { label: "Normal", color: "#39FF14" };
    if (b < 30) return { label: "Overweight", color: "#F59E0B" };
    return { label: "Obese", color: "#EF4444" };
  };

  const scrollTo = (id) => {
    const el = document.getElementById(id.toLowerCase());
    if (el) { el.scrollIntoView({ behavior: "smooth" }); setMenuOpen(false); setActiveNav(id); }
  };

  const reveal = (id) => visibleSections.has(id) ? "opacity-1 translate-0" : "";

  const style = {
    neon: "#39FF14",
    dark: "#050505",
    card: "rgba(255,255,255,0.04)",
    border: "rgba(57,255,20,0.2)",
  };

  return (
    <div style={{ fontFamily: "'Barlow Condensed', 'Bebas Neue', sans-serif", background: style.dark, color: "#fff", overflowX: "hidden", minHeight: "100vh" }}>
      <style>{`
        @import url('https://fonts.googleapis.com/css2?family=Barlow+Condensed:wght@300;400;600;700;900&family=Bebas+Neue&family=Barlow:wght@300;400;500&display=swap');
        * { margin:0; padding:0; box-sizing:border-box; }
        ::-webkit-scrollbar { width: 4px; }
        ::-webkit-scrollbar-track { background: #050505; }
        ::-webkit-scrollbar-thumb { background: #39FF14; border-radius: 2px; }
        html { scroll-behavior: smooth; }
        .fade-up { opacity: 0; transform: translateY(40px); transition: opacity 0.7s ease, transform 0.7s ease; }
        .fade-up.visible { opacity: 1; transform: translateY(0); }
        .neon-btn { background: #39FF14; color: #050505; border: none; padding: 14px 32px; font-family: 'Barlow Condensed', sans-serif; font-weight: 700; font-size: 16px; letter-spacing: 2px; text-transform: uppercase; cursor: pointer; border-radius: 2px; transition: all 0.3s; }
        .neon-btn:hover { background: #fff; box-shadow: 0 0 30px rgba(57,255,20,0.5); transform: translateY(-2px); }
        .outline-btn { background: transparent; color: #39FF14; border: 2px solid #39FF14; padding: 12px 30px; font-family: 'Barlow Condensed', sans-serif; font-weight: 700; font-size: 16px; letter-spacing: 2px; text-transform: uppercase; cursor: pointer; border-radius: 2px; transition: all 0.3s; }
        .outline-btn:hover { background: rgba(57,255,20,0.1); box-shadow: 0 0 20px rgba(57,255,20,0.3); transform: translateY(-2px); }
        .glass { background: rgba(255,255,255,0.04); backdrop-filter: blur(10px); border: 1px solid rgba(57,255,20,0.15); }
        .card-hover { transition: transform 0.3s, box-shadow 0.3s; }
        .card-hover:hover { transform: translateY(-8px); box-shadow: 0 20px 60px rgba(57,255,20,0.15); }
        .section-title { font-family: 'Bebas Neue', sans-serif; font-size: clamp(40px, 6vw, 72px); letter-spacing: 4px; line-height: 0.95; }
        .body-text { font-family: 'Barlow', sans-serif; font-weight: 300; line-height: 1.7; }
        input, textarea { background: rgba(255,255,255,0.06); border: 1px solid rgba(57,255,20,0.2); color: #fff; padding: 14px 18px; font-family: 'Barlow', sans-serif; font-size: 15px; border-radius: 4px; width: 100%; outline: none; transition: border-color 0.3s; }
        input:focus, textarea:focus { border-color: #39FF14; }
        input::placeholder, textarea::placeholder { color: rgba(255,255,255,0.3); }
        .stat-number { font-family: 'Bebas Neue', sans-serif; font-size: 64px; color: #39FF14; line-height: 1; }
        .pulse { animation: pulse 2s infinite; }
        @keyframes pulse { 0%,100% { opacity:1; } 50% { opacity:0.6; } }
        .neon-line { height: 3px; background: linear-gradient(90deg, transparent, #39FF14, transparent); border: none; }
        .whatsapp-float { position: fixed; bottom: 30px; right: 30px; z-index: 1000; width: 60px; height: 60px; background: #25D366; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 28px; cursor: pointer; box-shadow: 0 4px 20px rgba(37,211,102,0.5); animation: bounce 2s infinite; text-decoration: none; }
        @keyframes bounce { 0%,100% { transform: translateY(0); } 50% { transform: translateY(-8px); } }
        .grid-2 { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 24px; }
        .grid-3 { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 24px; }
        .bmi-slider { -webkit-appearance: none; height: 4px; background: rgba(57,255,20,0.2); border-radius: 2px; outline: none; cursor: pointer; }
        .bmi-slider::-webkit-slider-thumb { -webkit-appearance: none; width: 20px; height: 20px; background: #39FF14; border-radius: 50%; }
        @media (max-width: 768px) {
          .hero-btns { flex-direction: column; align-items: flex-start; }
          .stats-grid { grid-template-columns: repeat(2, 1fr); }
          .plans-grid { grid-template-columns: 1fr; }
        }
      `}</style>

      {/* STICKY NAV */}
      <nav style={{
        position: "fixed", top: 0, left: 0, right: 0, zIndex: 999,
        background: scrollY > 50 ? "rgba(5,5,5,0.97)" : "transparent",
        borderBottom: scrollY > 50 ? "1px solid rgba(57,255,20,0.15)" : "none",
        backdropFilter: scrollY > 50 ? "blur(20px)" : "none",
        transition: "all 0.4s",
        padding: "0 5%",
        display: "flex", alignItems: "center", justifyContent: "space-between", height: "72px"
      }}>
        <div style={{ display: "flex", alignItems: "center", gap: 12 }}>
          <div style={{ width: 40, height: 40, background: "#39FF14", borderRadius: 2, display: "flex", alignItems: "center", justifyContent: "center", fontFamily: "'Bebas Neue'", fontSize: 20, color: "#050505", fontWeight: 900 }}>SKT</div>
          <div>
            <div style={{ fontFamily: "'Bebas Neue'", fontSize: 20, letterSpacing: 3 }}>FITNESS WORLD</div>
            <div style={{ fontFamily: "'Barlow'", fontSize: 10, color: "#39FF14", letterSpacing: 2, lineHeight: 1 }}>BATHINDA, PUNJAB</div>
          </div>
        </div>

        {/* Desktop nav */}
        <div style={{ display: "flex", gap: 28, alignItems: "center" }} className="desktop-nav">
          {NAV_LINKS.map((l) => (
            <button key={l} onClick={() => scrollTo(l)} style={{
              background: "none", border: "none", color: activeNav === l ? "#39FF14" : "rgba(255,255,255,0.7)",
              fontFamily: "'Barlow Condensed'", fontWeight: 600, fontSize: 13, letterSpacing: 2,
              textTransform: "uppercase", cursor: "pointer", transition: "color 0.2s",
              borderBottom: activeNav === l ? "2px solid #39FF14" : "2px solid transparent",
              paddingBottom: 2
            }}>{l}</button>
          ))}
          <button className="neon-btn" style={{ padding: "10px 24px", fontSize: 13 }} onClick={() => scrollTo("Contact")}>Join Now</button>
        </div>

        {/* Mobile hamburger */}
        <button onClick={() => setMenuOpen(!menuOpen)} style={{ background: "none", border: "none", color: "#fff", fontSize: 28, cursor: "pointer", display: "none" }} className="hamburger">☰</button>
      </nav>

      {/* Mobile Menu */}
      {menuOpen && (
        <div style={{ position: "fixed", top: 72, left: 0, right: 0, zIndex: 998, background: "rgba(5,5,5,0.98)", padding: "20px 5%", borderBottom: "1px solid rgba(57,255,20,0.2)" }}>
          {NAV_LINKS.map((l) => (
            <div key={l} onClick={() => scrollTo(l)} style={{ padding: "14px 0", borderBottom: "1px solid rgba(255,255,255,0.05)", cursor: "pointer", fontFamily: "'Barlow Condensed'", fontWeight: 600, fontSize: 18, letterSpacing: 2, color: activeNav === l ? "#39FF14" : "#fff" }}>{l}</div>
          ))}
        </div>
      )}

      {/* ─── HERO ─── */}
      <section id="home" style={{ minHeight: "100vh", display: "flex", alignItems: "center", position: "relative", overflow: "hidden" }}>
        {/* Animated background */}
        <div style={{ position: "absolute", inset: 0, background: "linear-gradient(135deg, #050505 0%, #0a1a0a 50%, #050505 100%)" }} />
        <div style={{ position: "absolute", inset: 0, backgroundImage: "radial-gradient(circle at 20% 50%, rgba(57,255,20,0.06) 0%, transparent 50%), radial-gradient(circle at 80% 20%, rgba(57,255,20,0.04) 0%, transparent 40%)" }} />
        {/* Grid lines */}
        <div style={{ position: "absolute", inset: 0, backgroundImage: "linear-gradient(rgba(57,255,20,0.03) 1px, transparent 1px), linear-gradient(90deg, rgba(57,255,20,0.03) 1px, transparent 1px)", backgroundSize: "60px 60px" }} />

        {/* Big background text */}
        <div style={{ position: "absolute", right: "-5%", top: "50%", transform: "translateY(-50%)", fontFamily: "'Bebas Neue'", fontSize: "clamp(120px, 20vw, 260px)", color: "rgba(57,255,20,0.04)", letterSpacing: 10, userSelect: "none", lineHeight: 0.9 }}>
          FITNESS<br />WORLD
        </div>

        <div style={{ position: "relative", zIndex: 2, padding: "120px 8% 80px" }}>
          <div style={{ display: "inline-flex", alignItems: "center", gap: 8, background: "rgba(57,255,20,0.1)", border: "1px solid rgba(57,255,20,0.3)", padding: "8px 20px", borderRadius: 2, marginBottom: 32 }}>
            <span className="pulse" style={{ width: 8, height: 8, background: "#39FF14", borderRadius: "50%", display: "inline-block" }} />
            <span style={{ fontFamily: "'Barlow Condensed'", fontSize: 13, letterSpacing: 3, color: "#39FF14", fontWeight: 600 }}>NOW OPEN · BATHINDA, PUNJAB</span>
          </div>

          <h1 style={{ fontFamily: "'Bebas Neue'", fontSize: "clamp(60px, 10vw, 140px)", lineHeight: 0.88, letterSpacing: 4, marginBottom: 24, maxWidth: 800 }}>
            FORGE YOUR<br />
            <span style={{ color: "#39FF14", WebkitTextStroke: "0px", textShadow: "0 0 40px rgba(57,255,20,0.5)" }}>BEST</span>
            <br />BODY HERE
          </h1>

          <p className="body-text" style={{ fontSize: 18, color: "rgba(255,255,255,0.6)", maxWidth: 520, marginBottom: 48 }}>
            Premium fitness experience in Bathinda. State-of-the-art equipment, expert trainers, and a community that pushes you beyond your limits — all at a price that's unbeatable.
          </p>

          <div style={{ display: "flex", gap: 16, flexWrap: "wrap" }} className="hero-btns">
            <button className="neon-btn" onClick={() => scrollTo("Contact")} style={{ fontSize: 16, padding: "18px 44px" }}>JOIN NOW →</button>
            <button className="outline-btn" onClick={() => scrollTo("Plans")} style={{ fontSize: 16 }}>FREE TRIAL</button>
          </div>

          <div style={{ display: "flex", gap: 48, marginTop: 72, flexWrap: "wrap" }}>
            {[["500+", "Members"], ["3", "Expert Trainers"], ["5.0★", "Google Rating"], ["2+", "Years Strong"]].map(([n, l]) => (
              <div key={l}>
                <div style={{ fontFamily: "'Bebas Neue'", fontSize: 42, color: "#39FF14", lineHeight: 1 }}>{n}</div>
                <div style={{ fontFamily: "'Barlow'", fontSize: 13, color: "rgba(255,255,255,0.4)", letterSpacing: 2, textTransform: "uppercase", marginTop: 4 }}>{l}</div>
              </div>
            ))}
          </div>
        </div>

        {/* Scroll indicator */}
        <div style={{ position: "absolute", bottom: 40, left: "50%", transform: "translateX(-50%)", display: "flex", flexDirection: "column", alignItems: "center", gap: 8, animation: "bounce 2s infinite" }}>
          <div style={{ fontFamily: "'Barlow Condensed'", fontSize: 11, letterSpacing: 3, color: "rgba(255,255,255,0.3)" }}>SCROLL</div>
          <div style={{ width: 1, height: 40, background: "linear-gradient(to bottom, rgba(57,255,20,0.5), transparent)" }} />
        </div>
      </section>

      {/* ─── ABOUT ─── */}
      <section id="about" ref={(el) => (sectionRefs.current.about = el)} style={{ padding: "120px 8%", position: "relative" }}>
        <div style={{ position: "absolute", left: 0, top: "50%", width: "40%", height: 400, background: "radial-gradient(circle, rgba(57,255,20,0.04) 0%, transparent 70%)", pointerEvents: "none" }} />

        <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 80, alignItems: "center" }}>
          <div>
            <div style={{ fontFamily: "'Barlow Condensed'", fontSize: 13, letterSpacing: 4, color: "#39FF14", marginBottom: 16, fontWeight: 600 }}>OUR STORY</div>
            <h2 className="section-title" style={{ marginBottom: 24 }}>WHERE<br /><span style={{ color: "#39FF14" }}>LEGENDS</span><br />ARE MADE</h2>
            <p className="body-text" style={{ color: "rgba(255,255,255,0.65)", fontSize: 16, marginBottom: 24 }}>
              SKT Fitness World was born from a simple belief — premium fitness shouldn't cost a fortune. Founded in Bathinda, Punjab, we've built a sanctuary where every member, regardless of their starting point, gets access to world-class equipment, expert coaching, and an electric atmosphere.
            </p>
            <p className="body-text" style={{ color: "rgba(255,255,255,0.65)", fontSize: 16, marginBottom: 40 }}>
              Our mission is to transform lives through fitness. Our vision is to be Punjab's most loved gym — where results meet community, and where every workout brings you closer to the person you're meant to become.
            </p>
            <hr className="neon-line" style={{ width: 80, marginBottom: 40 }} />
            <div style={{ display: "flex", gap: 16 }}>
              <button className="neon-btn" onClick={() => scrollTo("Contact")}>Start Your Journey</button>
            </div>
          </div>

          <div>
            <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 20 }} className="stats-grid">
              {[
                ["500+", "Active Members", "Growing community"],
                ["3", "Expert Trainers", "Certified & dedicated"],
                ["5.0", "Google Rating", "7 reviews & counting"],
                ["2+", "Years Open", "Bathinda's finest"],
              ].map(([n, t, s]) => (
                <div key={t} className="glass card-hover" style={{ padding: "28px 24px", borderRadius: 4 }}>
                  <div className="stat-number">{n}</div>
                  <div style={{ fontFamily: "'Barlow Condensed'", fontWeight: 700, fontSize: 16, letterSpacing: 1, marginTop: 4 }}>{t}</div>
                  <div className="body-text" style={{ fontSize: 13, color: "rgba(255,255,255,0.4)", marginTop: 4 }}>{s}</div>
                </div>
              ))}
            </div>
          </div>
        </div>
      </section>

      {/* ─── SERVICES ─── */}
      <section id="services" ref={(el) => (sectionRefs.current.services = el)} style={{ padding: "120px 8%", background: "rgba(57,255,20,0.02)" }}>
        <div style={{ textAlign: "center", marginBottom: 80 }}>
          <div style={{ fontFamily: "'Barlow Condensed'", fontSize: 13, letterSpacing: 4, color: "#39FF14", marginBottom: 16, fontWeight: 600 }}>WHAT WE OFFER</div>
          <h2 className="section-title">OUR <span style={{ color: "#39FF14" }}>SERVICES</span></h2>
          <p className="body-text" style={{ color: "rgba(255,255,255,0.5)", marginTop: 16, maxWidth: 480, margin: "16px auto 0" }}>
            Every program is designed to deliver measurable results. Choose your path.
          </p>
        </div>

        <div className="grid-3">
          {SERVICES.map((s, i) => (
            <div key={s.title} className="glass card-hover" style={{ padding: "36px 32px", borderRadius: 4, animationDelay: `${i * 100}ms`, borderTop: "3px solid rgba(57,255,20,0.3)" }}>
              <div style={{ fontSize: 44, marginBottom: 20 }}>{s.icon}</div>
              <h3 style={{ fontFamily: "'Bebas Neue'", fontSize: 28, letterSpacing: 2, marginBottom: 12 }}>{s.title}</h3>
              <p className="body-text" style={{ color: "rgba(255,255,255,0.55)", fontSize: 15, lineHeight: 1.7 }}>{s.desc}</p>
              <div style={{ marginTop: 24, color: "#39FF14", fontFamily: "'Barlow Condensed'", fontWeight: 600, fontSize: 13, letterSpacing: 2, cursor: "pointer" }} onClick={() => scrollTo("Contact")}>LEARN MORE →</div>
            </div>
          ))}
        </div>
      </section>

      {/* ─── PLANS ─── */}
      <section id="plans" ref={(el) => (sectionRefs.current.plans = el)} style={{ padding: "120px 8%" }}>
        <div style={{ textAlign: "center", marginBottom: 80 }}>
          <div style={{ fontFamily: "'Barlow Condensed'", fontSize: 13, letterSpacing: 4, color: "#39FF14", marginBottom: 16, fontWeight: 600 }}>PRICING</div>
          <h2 className="section-title">MEMBERSHIP <span style={{ color: "#39FF14" }}>PLANS</span></h2>
          <p className="body-text" style={{ color: "rgba(255,255,255,0.5)", marginTop: 16, maxWidth: 480, margin: "16px auto 0" }}>
            Transparent pricing, no hidden fees. Invest in your health today.
          </p>
        </div>

        <div style={{ display: "grid", gridTemplateColumns: "repeat(auto-fit, minmax(280px, 1fr))", gap: 28 }} className="plans-grid">
          {PLANS.map((p) => (
            <div key={p.name} className="card-hover" style={{
              padding: "40px 32px",
              borderRadius: 4,
              position: "relative",
              background: p.popular ? "rgba(57,255,20,0.06)" : style.card,
              border: p.popular ? "2px solid #39FF14" : "1px solid rgba(57,255,20,0.15)",
              boxShadow: p.popular ? "0 0 60px rgba(57,255,20,0.1)" : "none",
            }}>
              {p.popular && (
                <div style={{ position: "absolute", top: -14, left: "50%", transform: "translateX(-50%)", background: "#39FF14", color: "#050505", fontFamily: "'Barlow Condensed'", fontWeight: 700, fontSize: 12, letterSpacing: 3, padding: "6px 20px", borderRadius: 2 }}>MOST POPULAR</div>
              )}
              <div style={{ fontFamily: "'Barlow Condensed'", fontWeight: 700, fontSize: 14, letterSpacing: 4, color: "rgba(255,255,255,0.5)", marginBottom: 8 }}>{p.name.toUpperCase()} PLAN</div>
              <div style={{ display: "flex", alignItems: "baseline", gap: 4, marginBottom: 8 }}>
                <span style={{ fontFamily: "'Bebas Neue'", fontSize: 64, color: p.popular ? "#39FF14" : "#fff", lineHeight: 1 }}>{p.price}</span>
                <span style={{ fontFamily: "'Barlow'", fontSize: 14, color: "rgba(255,255,255,0.4)" }}>{p.period}</span>
              </div>
              <hr style={{ border: "none", borderTop: "1px solid rgba(57,255,20,0.15)", margin: "24px 0" }} />
              <ul style={{ listStyle: "none", marginBottom: 36 }}>
                {p.features.map((f) => (
                  <li key={f} style={{ fontFamily: "'Barlow'", fontSize: 15, color: "rgba(255,255,255,0.7)", padding: "8px 0", borderBottom: "1px solid rgba(255,255,255,0.05)", display: "flex", alignItems: "center", gap: 10 }}>
                    <span style={{ color: "#39FF14", fontSize: 16 }}>✓</span> {f}
                  </li>
                ))}
              </ul>
              <button className={p.popular ? "neon-btn" : "outline-btn"} style={{ width: "100%", textAlign: "center" }} onClick={() => scrollTo("Contact")}>
                GET STARTED →
              </button>
            </div>
          ))}
        </div>
      </section>

      {/* ─── TRAINERS ─── */}
      <section id="trainers" ref={(el) => (sectionRefs.current.trainers = el)} style={{ padding: "120px 8%", background: "rgba(57,255,20,0.02)" }}>
        <div style={{ textAlign: "center", marginBottom: 80 }}>
          <div style={{ fontFamily: "'Barlow Condensed'", fontSize: 13, letterSpacing: 4, color: "#39FF14", marginBottom: 16, fontWeight: 600 }}>THE TEAM</div>
          <h2 className="section-title">MEET YOUR <span style={{ color: "#39FF14" }}>TRAINERS</span></h2>
        </div>

        <div className="grid-3">
          {TRAINERS.map((t) => (
            <div key={t.name} className="glass card-hover" style={{ padding: "44px 36px", borderRadius: 4, textAlign: "center" }}>
              <div style={{ width: 90, height: 90, background: "rgba(57,255,20,0.1)", borderRadius: "50%", margin: "0 auto 24px", display: "flex", alignItems: "center", justifyContent: "center", fontSize: 44, border: "2px solid rgba(57,255,20,0.3)" }}>{t.emoji}</div>
              <h3 style={{ fontFamily: "'Bebas Neue'", fontSize: 26, letterSpacing: 2, marginBottom: 6 }}>{t.name}</h3>
              <div style={{ fontFamily: "'Barlow Condensed'", fontWeight: 600, fontSize: 14, letterSpacing: 2, color: "#39FF14", marginBottom: 16 }}>{t.role}</div>
              <div style={{ display: "flex", gap: 12, justifyContent: "center", flexWrap: "wrap", marginBottom: 20 }}>
                {[t.cert, t.specialty].map((badge) => (
                  <span key={badge} style={{ background: "rgba(57,255,20,0.08)", border: "1px solid rgba(57,255,20,0.2)", padding: "5px 14px", borderRadius: 2, fontSize: 12, fontFamily: "'Barlow Condensed'", fontWeight: 600, letterSpacing: 1, color: "rgba(255,255,255,0.7)" }}>{badge}</span>
                ))}
              </div>
              <div style={{ fontFamily: "'Bebas Neue'", fontSize: 32, color: "#39FF14" }}>{t.exp}</div>
              <div style={{ fontFamily: "'Barlow'", fontSize: 12, color: "rgba(255,255,255,0.3)", letterSpacing: 2, textTransform: "uppercase" }}>Experience</div>
            </div>
          ))}
        </div>
      </section>

      {/* ─── TRANSFORMATIONS ─── */}
      <section id="transformations" ref={(el) => (sectionRefs.current.transformations = el)} style={{ padding: "120px 8%" }}>
        <div style={{ textAlign: "center", marginBottom: 80 }}>
          <div style={{ fontFamily: "'Barlow Condensed'", fontSize: 13, letterSpacing: 4, color: "#39FF14", marginBottom: 16, fontWeight: 600 }}>REAL RESULTS</div>
          <h2 className="section-title">MEMBER <span style={{ color: "#39FF14" }}>TRANSFORMATIONS</span></h2>
          <p className="body-text" style={{ color: "rgba(255,255,255,0.5)", marginTop: 16, maxWidth: 480, margin: "16px auto 0" }}>
            These are real members who committed. Their stories could be yours.
          </p>
        </div>

        <div className="grid-2">
          {TRANSFORMATIONS.map((t) => (
            <div key={t.name} className="glass card-hover" style={{ borderRadius: 4, overflow: "hidden" }}>
              <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", height: 200 }}>
                <div style={{ background: "linear-gradient(135deg, #1a1a1a, #0a0a0a)", display: "flex", flexDirection: "column", alignItems: "center", justifyContent: "center", borderRight: "1px solid rgba(57,255,20,0.1)" }}>
                  <div style={{ fontFamily: "'Barlow Condensed'", fontSize: 13, letterSpacing: 3, color: "rgba(255,255,255,0.3)", marginBottom: 8 }}>BEFORE</div>
                  <div style={{ fontFamily: "'Bebas Neue'", fontSize: 52, color: "rgba(255,255,255,0.6)" }}>{t.before}</div>
                  <div style={{ fontSize: 40 }}>😔</div>
                </div>
                <div style={{ background: "linear-gradient(135deg, #0a1a0a, #050505)", display: "flex", flexDirection: "column", alignItems: "center", justifyContent: "center" }}>
                  <div style={{ fontFamily: "'Barlow Condensed'", fontSize: 13, letterSpacing: 3, color: "#39FF14", marginBottom: 8 }}>AFTER</div>
                  <div style={{ fontFamily: "'Bebas Neue'", fontSize: 52, color: "#39FF14" }}>{t.after}</div>
                  <div style={{ fontSize: 40 }}>💪</div>
                </div>
              </div>
              <div style={{ padding: "24px 28px", borderTop: "1px solid rgba(57,255,20,0.1)" }}>
                <div style={{ display: "flex", justifyContent: "space-between", alignItems: "center" }}>
                  <div>
                    <div style={{ fontFamily: "'Bebas Neue'", fontSize: 22, letterSpacing: 2 }}>{t.name}</div>
                    <div className="body-text" style={{ color: "rgba(255,255,255,0.4)", fontSize: 13 }}>{t.time} journey</div>
                  </div>
                  <div style={{ fontFamily: "'Bebas Neue'", fontSize: 28, color: "#39FF14" }}>{t.loss || t.gain}</div>
                </div>
              </div>
            </div>
          ))}
        </div>
      </section>

      {/* ─── GALLERY ─── */}
      <section id="gallery" ref={(el) => (sectionRefs.current.gallery = el)} style={{ padding: "120px 8%", background: "rgba(57,255,20,0.02)" }}>
        <div style={{ textAlign: "center", marginBottom: 80 }}>
          <div style={{ fontFamily: "'Barlow Condensed'", fontSize: 13, letterSpacing: 4, color: "#39FF14", marginBottom: 16, fontWeight: 600 }}>INSIDE SKT</div>
          <h2 className="section-title">OUR <span style={{ color: "#39FF14" }}>GYM</span></h2>
        </div>

        <div style={{ display: "grid", gridTemplateColumns: "repeat(auto-fit, minmax(260px, 1fr))", gap: 16 }}>
          {GALLERY_ITEMS.map((g, i) => (
            <div key={g.label} className="card-hover" style={{
              height: i === 0 || i === 3 ? 280 : 220,
              background: g.bg,
              border: "1px solid rgba(57,255,20,0.1)",
              borderRadius: 4,
              display: "flex", flexDirection: "column", alignItems: "center", justifyContent: "center",
              padding: 24,
              position: "relative",
              overflow: "hidden"
            }}>
              <div style={{ position: "absolute", inset: 0, backgroundImage: "radial-gradient(circle at 50% 50%, rgba(57,255,20,0.04), transparent 70%)" }} />
              <div style={{ fontSize: 52, marginBottom: 16, position: "relative" }}>{g.emoji}</div>
              <div style={{ fontFamily: "'Bebas Neue'", fontSize: 22, letterSpacing: 2, textAlign: "center", position: "relative" }}>{g.label}</div>
              <div className="body-text" style={{ fontSize: 13, color: "rgba(255,255,255,0.4)", textAlign: "center", marginTop: 8, position: "relative" }}>{g.desc}</div>
            </div>
          ))}
        </div>
      </section>

      {/* ─── REVIEWS ─── */}
      <section id="reviews" ref={(el) => (sectionRefs.current.reviews = el)} style={{ padding: "120px 8%" }}>
        <div style={{ textAlign: "center", marginBottom: 80 }}>
          <div style={{ fontFamily: "'Barlow Condensed'", fontSize: 13, letterSpacing: 4, color: "#39FF14", marginBottom: 16, fontWeight: 600 }}>TESTIMONIALS</div>
          <h2 className="section-title">WHAT MEMBERS <span style={{ color: "#39FF14" }}>SAY</span></h2>
          <div style={{ display: "flex", alignItems: "center", justifyContent: "center", gap: 8, marginTop: 20 }}>
            <span style={{ fontFamily: "'Bebas Neue'", fontSize: 48, color: "#39FF14" }}>5.0</span>
            <div>
              <div style={{ color: "#39FF14", fontSize: 22, letterSpacing: 2 }}>★★★★★</div>
              <div style={{ fontFamily: "'Barlow'", fontSize: 13, color: "rgba(255,255,255,0.4)" }}>Google Reviews · 7 ratings</div>
            </div>
          </div>
        </div>

        {/* Animated featured review */}
        <div style={{ maxWidth: 700, margin: "0 auto 60px", position: "relative" }}>
          <div className="glass" style={{ padding: "48px 48px", borderRadius: 4, textAlign: "center", minHeight: 200 }}>
            <div style={{ fontSize: 48, color: "#39FF14", fontFamily: "'Bebas Neue'", lineHeight: 0.6, marginBottom: 24 }}>"</div>
            <p className="body-text" style={{ fontSize: 20, lineHeight: 1.7, color: "rgba(255,255,255,0.85)", marginBottom: 28 }}>{REVIEWS[reviewIdx].text}</p>
            <div style={{ fontFamily: "'Barlow Condensed'", fontWeight: 700, fontSize: 16, letterSpacing: 2 }}>{REVIEWS[reviewIdx].name}</div>
            <div style={{ color: "#39FF14", fontSize: 16, marginTop: 6 }}>{"★".repeat(REVIEWS[reviewIdx].rating)}</div>
          </div>
          <div style={{ display: "flex", gap: 8, justifyContent: "center", marginTop: 20 }}>
            {REVIEWS.map((_, i) => (
              <div key={i} onClick={() => setReviewIdx(i)} style={{ width: i === reviewIdx ? 32 : 8, height: 8, background: i === reviewIdx ? "#39FF14" : "rgba(57,255,20,0.2)", borderRadius: 4, cursor: "pointer", transition: "all 0.3s" }} />
            ))}
          </div>
        </div>

        {/* Review grid */}
        <div className="grid-2">
          {REVIEWS.map((r) => (
            <div key={r.name} className="glass card-hover" style={{ padding: "28px 32px", borderRadius: 4 }}>
              <div style={{ display: "flex", justifyContent: "space-between", alignItems: "flex-start", marginBottom: 16 }}>
                <div style={{ display: "flex", alignItems: "center", gap: 12 }}>
                  <div style={{ width: 44, height: 44, background: "rgba(57,255,20,0.1)", borderRadius: "50%", display: "flex", alignItems: "center", justifyContent: "center", fontFamily: "'Bebas Neue'", fontSize: 18, color: "#39FF14", border: "1px solid rgba(57,255,20,0.3)" }}>
                    {r.name.charAt(0)}
                  </div>
                  <div>
                    <div style={{ fontFamily: "'Barlow Condensed'", fontWeight: 700, fontSize: 16, letterSpacing: 1 }}>{r.name}</div>
                    <div style={{ fontFamily: "'Barlow'", fontSize: 12, color: "rgba(255,255,255,0.3)" }}>{r.date}</div>
                  </div>
                </div>
                <div style={{ color: "#39FF14", fontSize: 14 }}>{"★".repeat(r.rating)}</div>
              </div>
              <p className="body-text" style={{ fontSize: 14, color: "rgba(255,255,255,0.6)", lineHeight: 1.7 }}>{r.text}</p>
            </div>
          ))}
        </div>
      </section>

      {/* ─── BMI CALCULATOR ─── */}
      <section id="bmi" style={{ padding: "120px 8%", background: "rgba(57,255,20,0.02)" }}>
        <div style={{ maxWidth: 600, margin: "0 auto", textAlign: "center" }}>
          <div style={{ fontFamily: "'Barlow Condensed'", fontSize: 13, letterSpacing: 4, color: "#39FF14", marginBottom: 16, fontWeight: 600 }}>HEALTH TOOL</div>
          <h2 className="section-title" style={{ marginBottom: 20 }}>BMI <span style={{ color: "#39FF14" }}>CALCULATOR</span></h2>
          <p className="body-text" style={{ color: "rgba(255,255,255,0.5)", marginBottom: 48 }}>Check your Body Mass Index and understand where you stand.</p>

          <div className="glass" style={{ padding: "48px 40px", borderRadius: 4, textAlign: "left" }}>
            {[
              { label: "Height (cm)", value: height, min: 130, max: 220, step: 1, set: setHeight },
              { label: "Weight (kg)", value: weight, min: 30, max: 200, step: 1, set: setWeight },
              { label: "Age", value: age, min: 10, max: 80, step: 1, set: setAge },
            ].map(({ label, value, min, max, step, set }) => (
              <div key={label} style={{ marginBottom: 28 }}>
                <div style={{ display: "flex", justifyContent: "space-between", marginBottom: 10 }}>
                  <span style={{ fontFamily: "'Barlow Condensed'", fontWeight: 600, fontSize: 14, letterSpacing: 2, color: "rgba(255,255,255,0.7)" }}>{label}</span>
                  <span style={{ fontFamily: "'Bebas Neue'", fontSize: 22, color: "#39FF14" }}>{value}</span>
                </div>
                <input type="range" className="bmi-slider" min={min} max={max} step={step} value={value}
                  onChange={(e) => { set(Number(e.target.value)); setBmi(null); }}
                  style={{ width: "100%" }} />
              </div>
            ))}

            <button className="neon-btn" onClick={calcBMI} style={{ width: "100%", padding: "18px", fontSize: 17, marginTop: 8 }}>CALCULATE BMI</button>

            {bmi && (
              <div style={{ marginTop: 36, padding: "28px", background: "rgba(57,255,20,0.06)", border: "1px solid rgba(57,255,20,0.3)", borderRadius: 4, textAlign: "center" }}>
                <div style={{ fontFamily: "'Bebas Neue'", fontSize: 80, color: "#39FF14", lineHeight: 1 }}>{bmi}</div>
                <div style={{ fontFamily: "'Barlow Condensed'", fontWeight: 700, fontSize: 20, letterSpacing: 3, color: bmiCategory(bmi).color, marginTop: 4 }}>{bmiCategory(bmi).label}</div>
                <div className="body-text" style={{ color: "rgba(255,255,255,0.5)", marginTop: 12, fontSize: 14 }}>
                  {bmi < 18.5 && "You're underweight. Our nutrition coaches can help you gain healthy weight."}
                  {bmi >= 18.5 && bmi < 25 && "You're in the normal range. Keep it up with our maintenance programs!"}
                  {bmi >= 25 && bmi < 30 && "You're slightly overweight. Our weight loss programs can help you reach your goal."}
                  {bmi >= 30 && "Let's work together. Our trainers have helped many achieve incredible transformations."}
                </div>
                <button className="neon-btn" onClick={() => scrollTo("Contact")} style={{ marginTop: 20, fontSize: 14, padding: "12px 28px" }}>TALK TO A TRAINER →</button>
              </div>
            )}
          </div>
        </div>
      </section>

      {/* ─── CONTACT ─── */}
      <section id="contact" ref={(el) => (sectionRefs.current.contact = el)} style={{ padding: "120px 8%" }}>
        <div style={{ textAlign: "center", marginBottom: 80 }}>
          <div style={{ fontFamily: "'Barlow Condensed'", fontSize: 13, letterSpacing: 4, color: "#39FF14", marginBottom: 16, fontWeight: 600 }}>GET IN TOUCH</div>
          <h2 className="section-title">START <span style={{ color: "#39FF14" }}>TODAY</span></h2>
        </div>

        <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 60, alignItems: "start" }}>
          {/* Form */}
          <div>
            <h3 style={{ fontFamily: "'Bebas Neue'", fontSize: 28, letterSpacing: 3, marginBottom: 32 }}>SEND US A MESSAGE</h3>
            {formSent ? (
              <div className="glass" style={{ padding: "48px", borderRadius: 4, textAlign: "center" }}>
                <div style={{ fontSize: 60, marginBottom: 20 }}>✅</div>
                <div style={{ fontFamily: "'Bebas Neue'", fontSize: 32, color: "#39FF14", letterSpacing: 2 }}>MESSAGE SENT!</div>
                <p className="body-text" style={{ color: "rgba(255,255,255,0.5)", marginTop: 12 }}>We'll call you back within 24 hours. Get ready to transform!</p>
              </div>
            ) : (
              <div style={{ display: "flex", flexDirection: "column", gap: 16 }}>
                <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 16 }}>
                  <input placeholder="Your Name" value={formData.name} onChange={(e) => setFormData({ ...formData, name: e.target.value })} />
                  <input placeholder="Phone Number" value={formData.phone} onChange={(e) => setFormData({ ...formData, phone: e.target.value })} />
                </div>
                <input placeholder="Email Address" value={formData.email} onChange={(e) => setFormData({ ...formData, email: e.target.value })} />
                <textarea rows={5} placeholder="Tell us your fitness goals..." value={formData.message} onChange={(e) => setFormData({ ...formData, message: e.target.value })} />
                <button className="neon-btn" onClick={() => { if (formData.name && formData.phone) setFormSent(true); }} style={{ fontSize: 16, padding: "18px" }}>SEND MESSAGE →</button>
              </div>
            )}
          </div>

          {/* Info */}
          <div>
            <h3 style={{ fontFamily: "'Bebas Neue'", fontSize: 28, letterSpacing: 3, marginBottom: 32 }}>VISIT US</h3>
            <div style={{ display: "flex", flexDirection: "column", gap: 20, marginBottom: 40 }}>
              {[
                { icon: "📍", label: "Address", value: "Dadi Poti Park, Near, Bathinda, Punjab 151001" },
                { icon: "📞", label: "Phone", value: "+91 81465 62930" },
                { icon: "📧", label: "Email", value: "sktfitnessworld@gmail.com" },
                { icon: "⏰", label: "Hours", value: "Mon–Sat: 5:00 AM – 9:30 PM\nSunday: 6:00 AM – 8:00 PM" },
              ].map((item) => (
                <div key={item.label} className="glass" style={{ padding: "20px 24px", borderRadius: 4, display: "flex", gap: 16, alignItems: "flex-start" }}>
                  <span style={{ fontSize: 24, flexShrink: 0 }}>{item.icon}</span>
                  <div>
                    <div style={{ fontFamily: "'Barlow Condensed'", fontWeight: 700, fontSize: 13, letterSpacing: 2, color: "#39FF14", marginBottom: 4 }}>{item.label}</div>
                    <div className="body-text" style={{ fontSize: 15, color: "rgba(255,255,255,0.7)", whiteSpace: "pre-line" }}>{item.value}</div>
                  </div>
                </div>
              ))}
            </div>

            {/* Map embed */}
            <div style={{ borderRadius: 4, overflow: "hidden", border: "1px solid rgba(57,255,20,0.2)", height: 200 }}>
              <iframe
                src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3441.1234567890!2d74.9333333!3d30.2000000!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x391724f0000000%3A0x1234567890abcdef!2sSKT%20Fitness%20World!5e0!3m2!1sen!2sin!4v1000000000000"
                width="100%" height="200" style={{ border: 0, filter: "invert(90%) hue-rotate(180deg)" }}
                allowFullScreen loading="lazy"
              />
            </div>
          </div>
        </div>
      </section>

      {/* ─── FOOTER ─── */}
      <footer style={{ background: "#000", borderTop: "1px solid rgba(57,255,20,0.15)", padding: "60px 8% 30px" }}>
        <div style={{ display: "grid", gridTemplateColumns: "repeat(auto-fit, minmax(200px, 1fr))", gap: 48, marginBottom: 60 }}>
          <div>
            <div style={{ display: "flex", alignItems: "center", gap: 12, marginBottom: 20 }}>
              <div style={{ width: 44, height: 44, background: "#39FF14", borderRadius: 2, display: "flex", alignItems: "center", justifyContent: "center", fontFamily: "'Bebas Neue'", fontSize: 22, color: "#050505" }}>SKT</div>
              <div style={{ fontFamily: "'Bebas Neue'", fontSize: 22, letterSpacing: 3 }}>FITNESS WORLD</div>
            </div>
            <p className="body-text" style={{ fontSize: 14, color: "rgba(255,255,255,0.4)", lineHeight: 1.8 }}>
              Bathinda's premium fitness destination. Transform your body, elevate your mindset, live your best life.
            </p>
            <div style={{ display: "flex", gap: 12, marginTop: 24 }}>
              {["📘", "📸", "▶️", "📱"].map((icon, i) => (
                <div key={i} style={{ width: 40, height: 40, background: "rgba(57,255,20,0.08)", border: "1px solid rgba(57,255,20,0.2)", borderRadius: 2, display: "flex", alignItems: "center", justifyContent: "center", fontSize: 18, cursor: "pointer" }}>{icon}</div>
              ))}
            </div>
          </div>

          <div>
            <div style={{ fontFamily: "'Barlow Condensed'", fontWeight: 700, fontSize: 14, letterSpacing: 3, color: "#39FF14", marginBottom: 20 }}>QUICK LINKS</div>
            {NAV_LINKS.map((l) => (
              <div key={l} onClick={() => scrollTo(l)} style={{ fontFamily: "'Barlow'", fontSize: 15, color: "rgba(255,255,255,0.5)", padding: "6px 0", cursor: "pointer", transition: "color 0.2s", borderBottom: "1px solid rgba(255,255,255,0.05)" }}
                onMouseEnter={(e) => (e.target.style.color = "#39FF14")}
                onMouseLeave={(e) => (e.target.style.color = "rgba(255,255,255,0.5)")}
              >{l}</div>
            ))}
          </div>

          <div>
            <div style={{ fontFamily: "'Barlow Condensed'", fontWeight: 700, fontSize: 14, letterSpacing: 3, color: "#39FF14", marginBottom: 20 }}>CONTACT</div>
            <div className="body-text" style={{ fontSize: 14, color: "rgba(255,255,255,0.5)", lineHeight: 2 }}>
              📍 Dadi Poti Park, Bathinda<br />
              📞 +91 81465 62930<br />
              ⭐ 5.0/5 Google Rating<br />
              ⏰ Open until 9:30 PM
            </div>
          </div>

          <div>
            <div style={{ fontFamily: "'Barlow Condensed'", fontWeight: 700, fontSize: 14, letterSpacing: 3, color: "#39FF14", marginBottom: 20 }}>NEWSLETTER</div>
            <p className="body-text" style={{ fontSize: 14, color: "rgba(255,255,255,0.4)", marginBottom: 16 }}>Get fitness tips, offers & updates.</p>
            <div style={{ display: "flex", gap: 0 }}>
              <input placeholder="Your email" style={{ borderRadius: "4px 0 0 4px", borderRight: "none", flex: 1 }} />
              <button className="neon-btn" style={{ borderRadius: "0 4px 4px 0", padding: "14px 20px", fontSize: 13, whiteSpace: "nowrap" }}>JOIN</button>
            </div>
          </div>
        </div>

        <hr className="neon-line" style={{ marginBottom: 24 }} />

        <div style={{ display: "flex", justifyContent: "space-between", alignItems: "center", flexWrap: "wrap", gap: 16 }}>
          <div className="body-text" style={{ fontSize: 13, color: "rgba(255,255,255,0.3)" }}>© 2024 SKT Fitness World, Bathinda, Punjab. All rights reserved.</div>
          <div className="body-text" style={{ fontSize: 13, color: "rgba(255,255,255,0.3)" }}>Designed with 💚 for Bathinda's fitness community</div>
        </div>
      </footer>

      {/* WhatsApp Float */}
      <a href="https://wa.me/918146562930?text=Hi%20SKT%20Fitness%20World!%20I'm%20interested%20in%20joining." target="_blank" rel="noopener noreferrer" className="whatsapp-float" title="Chat on WhatsApp">
        💬
      </a>
    </div>
  );
}

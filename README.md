import React, { useMemo } from "react";
import { motion } from "framer-motion";
import {
  ShieldCheck,
  Activity,
  HeartPulse,
  MapPin,
  Sparkles,
  LineChart,
  Lock,
  ArrowRight,
  Smartphone,
} from "lucide-react";

/**
 * Magnus — marketing website (single page)
 * - Dark theme with red accents
 * - Subtle animated football-inspired background
 * - Sections: Hero, Product, AI Training, Security, FAQ, CTA
 *
 * Drop this into a Next.js/React page.
 * Tailwind assumed.
 */

const Section = ({ id, title, subtitle, children }) => (
  <section id={id} className="relative mx-auto w-full max-w-6xl px-4 py-16 sm:px-6">
    <div className="mb-8">
      <h2 className="text-2xl font-semibold tracking-tight text-white sm:text-3xl">{title}</h2>
      {subtitle ? (
        <p className="mt-2 max-w-2xl text-sm leading-relaxed text-white/70 sm:text-base">{subtitle}</p>
      ) : null}
    </div>
    {children}
  </section>
);

const Pill = ({ children }) => (
  <span className="inline-flex items-center gap-2 rounded-full border border-white/10 bg-white/5 px-3 py-1 text-xs text-white/80">
    {children}
  </span>
);

const Card = ({ icon: Icon, title, text }) => (
  <div className="group relative overflow-hidden rounded-2xl border border-white/10 bg-white/5 p-6 shadow-sm">
    <div className="absolute inset-0 opacity-0 transition-opacity duration-300 group-hover:opacity-100">
      <div className="pointer-events-none absolute -left-24 -top-24 h-64 w-64 rounded-full bg-red-600/10 blur-2xl" />
      <div className="pointer-events-none absolute -bottom-24 -right-24 h-64 w-64 rounded-full bg-red-500/10 blur-2xl" />
    </div>
    <div className="relative">
      <div className="mb-4 inline-flex h-11 w-11 items-center justify-center rounded-xl border border-white/10 bg-black/40">
        <Icon className="h-5 w-5 text-red-500" />
      </div>
      <h3 className="text-base font-semibold text-white">{title}</h3>
      <p className="mt-2 text-sm leading-relaxed text-white/70">{text}</p>
    </div>
  </div>
);

function AnimatedFootballBackground() {
  // Generate deterministic positions
  const balls = useMemo(
    () =>
      Array.from({ length: 10 }).map((_, i) => ({
        id: i,
        x: (i * 13) % 100,
        y: (i * 19) % 100,
        s: 0.7 + ((i * 7) % 10) / 10,
        d: 10 + ((i * 5) % 12),
        a: 12 + ((i * 3) % 10),
      })),
    []
  );

  return (
    <div aria-hidden className="pointer-events-none absolute inset-0 overflow-hidden">
      {/* Base glow */}
      <div className="absolute inset-0 bg-gradient-to-b from-black via-black to-black" />
      <div className="absolute inset-0 opacity-60 [background:radial-gradient(80%_60%_at_50%_0%,rgba(239,68,68,0.18),transparent_70%)]" />
      <div className="absolute inset-0 opacity-40 [background:radial-gradient(60%_60%_at_20%_80%,rgba(239,68,68,0.14),transparent_65%)]" />

      {/* Subtle noise */}
      <div className="absolute inset-0 opacity-[0.08] mix-blend-overlay [background-image:url('data:image/svg+xml,%3Csvg%20xmlns=%22http://www.w3.org/2000/svg%22%20width=%22120%22%20height=%22120%22%3E%3Cfilter%20id=%22n%22%3E%3CfeTurbulence%20type=%22fractalNoise%22%20baseFrequency=%220.9%22%20numOctaves=%223%22%20stitchTiles=%22stitch%22/%3E%3C/filter%3E%3Crect%20width=%22120%22%20height=%22120%22%20filter=%22url(%23n)%22%20opacity=%220.55%22/%3E%3C/svg%3E')]" />

      {/* Moving footballs (very subtle) */}
      {balls.map((b) => (
        <motion.div
          key={b.id}
          className="absolute"
          style={{ left: `${b.x}%`, top: `${b.y}%`, transform: `scale(${b.s})` }}
          initial={{ y: 0, x: 0, rotate: 0, opacity: 0.0 }}
          animate={{
            y: [0, -b.a, 0, b.a, 0],
            x: [0, b.a, 0, -b.a, 0],
            rotate: [0, 180, 360],
            opacity: [0.0, 0.12, 0.18, 0.12, 0.0],
          }}
          transition={{ duration: b.d, repeat: Infinity, ease: "easeInOut" }}
        >
          <div className="relative h-16 w-16 rounded-full border border-white/10 bg-white/5 backdrop-blur-sm">
            {/* football seams */}
            <div className="absolute inset-0 rounded-full [background:radial-gradient(circle_at_30%_30%,rgba(255,255,255,0.22),transparent_45%)]" />
            <div className="absolute left-1/2 top-1/2 h-10 w-10 -translate-x-1/2 -translate-y-1/2 rounded-full border border-white/10" />
            <div className="absolute left-1/2 top-1/2 h-6 w-6 -translate-x-1/2 -translate-y-1/2 rounded-full border border-white/10" />
            <div className="absolute left-1/2 top-1/2 h-[2px] w-10 -translate-x-1/2 -translate-y-1/2 bg-white/10" />
          </div>
        </motion.div>
      ))}

      {/* Vignette */}
      <div className="absolute inset-0 [background:radial-gradient(120%_80%_at_50%_50%,transparent_40%,rgba(0,0,0,0.92)_100%)]" />
    </div>
  );
}

export default function MagnusWebsite() {
  const features = [
    {
      icon: Activity,
      title: "Alles op één plek",
      text: "Verzamel en visualiseer sportdata uit Apple Health en GPS-tracking providers in één overzichtelijke timeline.",
    },
    {
      icon: LineChart,
      title: "Inzichten die je snapt",
      text: "Trends per week/maand, load, intensiteit en herstel—zonder gedoe. Klaar voor trainingen én wedstrijden.",
    },
    {
      icon: Sparkles,
      title: "AI trainingsadvies",
      text: "Van data naar actie: advies en weekplanning afgestemd op jouw doelen, beschikbaarheid en belastbaarheid.",
    },
    {
      icon: HeartPulse,
      title: "Performance metrics",
      text: "Kernmetrics zoals duur, afstand, hartslagzones en sessiefrequentie—consistent, ook met meerdere bronnen.",
    },
    {
      icon: ShieldCheck,
      title: "Privacy-first",
      text: "Minimale permissies, versleuteling en duidelijke controle over jouw data. Jij bepaalt wat gekoppeld is.",
    },
    {
      icon: MapPin,
      title: "GPS import",
      text: "Importeer activiteiten uit externe providers. Magnus normaliseert alles naar één datamodel.",
    },
  ];

  const faqs = [
    {
      q: "Welke data leest Magnus uit Apple Health?",
      a: "In de eerste versie richten we ons op workouts (duur, type, afstand, calorieën) en waar beschikbaar hartslag-samenvattingen. We vragen alleen om wat nodig is.",
    },
    {
      q: "Kan ik mijn data verwijderen?",
      a: "Ja. In je profiel kun je koppelingen verbreken en je data exporteren of volledig laten verwijderen.",
    },
    {
      q: "Is het AI-advies medisch?",
      a: "Nee. Het is trainingsbegeleiding op basis van je sportdata en doelen. Bij blessures of klachten adviseren we altijd een professional.",
    },
  ];

  return (
    <div className="min-h-screen bg-black text-white">
      <header className="relative">
        <AnimatedFootballBackground />

        {/* Top bar */}
        <div className="relative mx-auto flex w-full max-w-6xl items-center justify-between px-4 py-5 sm:px-6">
          <div className="flex items-center gap-3">
            <div className="grid h-10 w-10 place-items-center rounded-2xl border border-white/10 bg-white/5 shadow-sm">
              <span className="text-sm font-semibold tracking-tight">M</span>
            </div>
            <div>
              <div className="text-sm font-semibold leading-none">Magnus</div>
              <div className="mt-1 text-xs text-white/60">Collect • Store • Visualize • Advise</div>
            </div>
          </div>

          <nav className="hidden items-center gap-6 text-sm text-white/80 md:flex">
            <a href="#product" className="hover:text-white">Product</a>
            <a href="#ai" className="hover:text-white">AI Training</a>
            <a href="#security" className="hover:text-white">Security</a>
            <a href="#faq" className="hover:text-white">FAQ</a>
          </nav>

          <div className="flex items-center gap-2">
            <a
              href="#cta"
              className="inline-flex items-center gap-2 rounded-xl border border-white/10 bg-white/5 px-4 py-2 text-sm text-white/90 hover:bg-white/10"
            >
              Vraag demo
              <ArrowRight className="h-4 w-4 text-red-500" />
            </a>
          </div>
        </div>

        {/* Hero */}
        <div className="relative mx-auto w-full max-w-6xl px-4 pb-16 pt-10 sm:px-6 sm:pb-20">
          <div className="grid gap-10 md:grid-cols-2 md:items-center">
            <div>
              <div className="flex flex-wrap gap-2">
                <Pill>
                  <Lock className="h-3.5 w-3.5 text-red-500" /> Privacy-first
                </Pill>
                <Pill>
                  <Smartphone className="h-3.5 w-3.5 text-red-500" /> Mobile-first
                </Pill>
                <Pill>
                  <Sparkles className="h-3.5 w-3.5 text-red-500" /> AI training advice
                </Pill>
              </div>

              <h1 className="mt-6 text-4xl font-semibold tracking-tight sm:text-5xl">
                Magnus maakt van jouw sportdata <span className="text-red-500">trainingsactie</span>.
              </h1>
              <p className="mt-4 max-w-xl text-sm leading-relaxed text-white/70 sm:text-base">
                Verbind Apple Health en GPS-providers, zie duidelijke dashboards, en ontvang advies dat past bij jouw doelen—
                van belastbaarheid tot match readiness.
              </p>

              <div className="mt-8 flex flex-col gap-3 sm:flex-row">
                <a
                  href="#cta"
                  className="inline-flex items-center justify-center gap-2 rounded-2xl bg-red-600 px-5 py-3 text-sm font-semibold text-white shadow-sm hover:bg-red-500"
                >
                  Start met Prototype 1
                  <ArrowRight className="h-4 w-4" />
                </a>
                <a
                  href="#product"
                  className="inline-flex items-center justify-center gap-2 rounded-2xl border border-white/10 bg-white/5 px-5 py-3 text-sm font-semibold text-white/90 hover:bg-white/10"
                >
                  Bekijk features
                </a>
              </div>

              <p className="mt-5 text-xs text-white/50">
                Focus: verzamelen • veilig opslaan • visualiseren • AI-advies voor trainingen.
              </p>
            </div>

            {/* Mock app preview */}
            <div className="relative">
              <motion.div
                initial={{ opacity: 0, y: 16 }}
                animate={{ opacity: 1, y: 0 }}
                transition={{ duration: 0.6, ease: "easeOut" }}
                className="relative mx-auto w-full max-w-md"
              >
                <div className="absolute -inset-6 rounded-[2rem] bg-red-600/10 blur-2xl" />
                <div className="relative overflow-hidden rounded-[2rem] border border-white/10 bg-black/60 shadow-xl backdrop-blur">
                  <div className="flex items-center justify-between border-b border-white/10 px-5 py-4">
                    <div>
                      <div className="text-xs text-white/60">Welcome back</div>
                      <div className="text-sm font-semibold">Your Dashboard</div>
                    </div>
                    <div className="h-9 w-9 rounded-xl border border-white/10 bg-white/5" />
                  </div>

                  <div className="space-y-4 p-5">
                    <div className="grid grid-cols-3 gap-3">
                      {["Load", "HR Zones", "Sessions"].map((t) => (
                        <div key={t} className="rounded-2xl border border-white/10 bg-white/5 p-3">
                          <div className="text-[10px] text-white/60">{t}</div>
                          <div className="mt-1 h-2 w-full rounded-full bg-white/10">
                            <div className="h-2 w-2/3 rounded-full bg-red-600/60" />
                          </div>
                        </div>
                      ))}
                    </div>

                    <div className="rounded-2xl border border-white/10 bg-white/5 p-4">
                      <div className="text-xs font-semibold">Weekly trend</div>
                      <div className="mt-3 h-28 w-full rounded-xl bg-gradient-to-tr from-white/5 to-white/0" />
                    </div>

                    <div className="grid grid-cols-4 gap-2">
                      {[
                        { label: "Dashboard", active: true },
                        { label: "Tests" },
                        { label: "Training" },
                        { label: "Profile" },
                      ].map((b) => (
                        <div
                          key={b.label}
                          className={`rounded-2xl px-3 py-2 text-center text-[10px] border ${
                            b.active
                              ? "border-red-600/40 bg-red-600/10 text-white"
                              : "border-white/10 bg-white/5 text-white/70"
                          }`}
                        >
                          {b.label}
                        </div>
                      ))}
                    </div>
                  </div>
                </div>
              </motion.div>
            </div>
          </div>
        </div>
      </header>

      <main>
        <Section
          id="product"
          title="Wat Magnus doet"
          subtitle="De kern: sportdata verzamelen, veilig opslaan en helder visualiseren—zodat je betere keuzes maakt in training en herstel."
        >
          <div className="grid gap-4 sm:grid-cols-2 lg:grid-cols-3">
            {features.map((f) => (
              <Card key={f.title} icon={f.icon} title={f.title} text={f.text} />
            ))}
          </div>
        </Section>

        <Section
          id="ai"
          title="AI Training: van data naar weekplan"
          subtitle="Magnus combineert jouw recente belasting, intensiteit en beschikbaarheid met je doelen. Het resultaat: advies dat praktisch uitvoerbaar is."
        >
          <div className="grid gap-6 md:grid-cols-2">
            <div className="rounded-2xl border border-white/10 bg-white/5 p-6">
              <h3 className="text-base font-semibold">Hoe het werkt (Prototype 1)</h3>
              <ul className="mt-4 space-y-3 text-sm text-white/70">
                <li className="flex gap-3">
                  <span className="mt-1 h-2 w-2 rounded-full bg-red-500" />
                  Metrics: sessies/week, minuten, afstand, (waar beschikbaar) HR-zones.
                </li>
                <li className="flex gap-3">
                  <span className="mt-1 h-2 w-2 rounded-full bg-red-500" />
                  Doelen & constraints: endurance, speed, strength, return-to-play, match readiness.
                </li>
                <li className="flex gap-3">
                  <span className="mt-1 h-2 w-2 rounded-full bg-red-500" />
                  Output: weekadvies + sessiesuggesties, met een korte “waarom”-uitleg.
                </li>
              </ul>
            </div>

            <div className="rounded-2xl border border-white/10 bg-white/5 p-6">
              <h3 className="text-base font-semibold">Voorbeeld advies</h3>
              <div className="mt-4 space-y-3 rounded-2xl border border-white/10 bg-black/30 p-4 text-sm text-white/80">
                <p className="text-white/90">
                  <span className="font-semibold">Doel:</span> speed + match readiness (3 dagen/week)
                </p>
                <p>
                  <span className="font-semibold">Weekfocus:</span> 1x interval (kort), 1x tempo, 1x herstel + techniek.
                </p>
                <p className="text-white/70">
                  Waarom: vorige week daalde je high-intensity tijd, terwijl je totale volume stabiel bleef. We bouwen prikkel op
                  zonder extra belasting.
                </p>
              </div>
              <p className="mt-3 text-xs text-white/50">*Geen medisch advies. Bij blessures: rustiger opbouwen en raadpleeg een professional.</p>
            </div>
          </div>
        </Section>

        <Section
          id="security"
          title="Security & privacy"
          subtitle="Sport- en gezondheidsdata zijn gevoelig. Daarom is Magnus privacy-first ontworpen."
        >
          <div className="grid gap-4 md:grid-cols-3">
            <Card
              icon={Lock}
              title="Versleuteling"
              text="TLS in transit, encryptie at rest. Tokens/credentials worden versleuteld opgeslagen."
            />
            <Card
              icon={ShieldCheck}
              title="Minimale toegang"
              text="We vragen alleen permissies die nodig zijn voor de functies die jij gebruikt."
            />
            <Card
              icon={Smartphone}
              title="Jij hebt controle"
              text="Koppelingen verbreken, exporteren en verwijderen van data vanuit je profiel."
            />
          </div>
        </Section>

        <Section id="faq" title="FAQ" subtitle="Snelle antwoorden op de meest voorkomende vragen.">
          <div className="grid gap-4 md:grid-cols-3">
            {faqs.map((f) => (
              <div key={f.q} className="rounded-2xl border border-white/10 bg-white/5 p-6">
                <div className="text-sm font-semibold">{f.q}</div>
                <div className="mt-2 text-sm leading-relaxed text-white/70">{f.a}</div>
              </div>
            ))}
          </div>
        </Section>

        <section id="cta" className="relative">
          <div className="mx-auto w-full max-w-6xl px-4 py-16 sm:px-6">
            <div className="relative overflow-hidden rounded-3xl border border-white/10 bg-white/5 p-8 shadow-sm sm:p-10">
              <div className="absolute -left-24 -top-24 h-72 w-72 rounded-full bg-red-600/15 blur-3xl" />
              <div className="absolute -bottom-24 -right-24 h-72 w-72 rounded-full bg-red-500/15 blur-3xl" />

              <div className="relative grid gap-8 md:grid-cols-2 md:items-center">
                <div>
                  <h3 className="text-2xl font-semibold tracking-tight">Klaar om Magnus live te zien?</h3>
                  <p className="mt-2 text-sm leading-relaxed text-white/70">
                    Vraag een demo aan of start met de eerste prototype-website + app flow. We bouwen stap voor stap: connect → import →
                    dashboards → AI training.
                  </p>
                  <div className="mt-5 flex flex-wrap gap-2">
                    <Pill>Dashboard</Pill>
                    <Pill>Tests</Pill>
                    <Pill>Training</Pill>
                    <Pill>Profile</Pill>
                  </div>
                </div>

                <form
                  onSubmit={(e) => e.preventDefault()}
                  className="relative rounded-2xl border border-white/10 bg-black/30 p-5"
                >
                  <label className="text-xs text-white/70">Email</label>
                  <input
                    className="mt-2 w-full rounded-xl border border-white/10 bg-black/40 px-4 py-3 text-sm text-white placeholder:text-white/40 outline-none focus:border-red-600/50"
                    placeholder="jij@bedrijf.nl"
                    type="email"
                    required
                  />
                  <label className="mt-4 block text-xs text-white/70">Waar wil je op focussen?</label>
                  <select className="mt-2 w-full rounded-xl border border-white/10 bg-black/40 px-4 py-3 text-sm text-white outline-none focus:border-red-600/50">
                    <option>Prototype 1 (basis functies)</option>
                    <option>Apple Health / HealthKit integratie</option>
                    <option>GPS provider API integratie</option>
                    <option>AI trainingsadvies</option>
                  </select>

                  <button
                    className="mt-5 inline-flex w-full items-center justify-center gap-2 rounded-2xl bg-red-600 px-5 py-3 text-sm font-semibold text-white hover:bg-red-500"
                    type="submit"
                  >
                    Verstuur
                    <ArrowRight className="h-4 w-4" />
                  </button>

                  <p className="mt-3 text-center text-xs text-white/50">
                    Door te versturen ga je akkoord met het verwerken van je gegevens voor contactdoeleinden.
                  </p>
                </form>
              </div>
            </div>
          </div>
        </section>
      </main>

      <footer className="border-t border-white/10">
        <div className="mx-auto flex w-full max-w-6xl flex-col gap-3 px-4 py-10 text-sm text-white/60 sm:flex-row sm:items-center sm:justify-between sm:px-6">
          <div className="flex items-center gap-2">
            <div className="grid h-8 w-8 place-items-center rounded-xl border border-white/10 bg-white/5">
              <span className="text-xs font-semibold">M</span>
            </div>
            <span>© {new Date().getFullYear()} Magnus</span>
          </div>
          <div className="flex flex-wrap gap-5">
            <a href="#security" className="hover:text-white">Privacy</a>
            <a href="#faq" className="hover:text-white">FAQ</a>
            <a href="#cta" className="hover:text-white">Contact</a>
          </div>
        </div>
      </footer>
    </div>
  );
}

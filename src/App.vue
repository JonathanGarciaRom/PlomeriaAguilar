<script setup lang="ts">
import { computed, ref } from 'vue'

const WHATSAPP_NUMBER = '222 407 7936'
const PHONE_NUMBER = '+52 222 407 7936'

const stats = [
  { value: '10+', label: 'Años de experiencia' },
  { value: '500+', label: 'Servicios realizados' },
  { value: '24/7', label: 'Emergencias' },
  { value: '100%', label: 'Compromiso' },
]

const services = [
  {
    title: 'Reparación de fugas',
    description:
      'Detectamos y reparamos fugas visibles y ocultas para evitar daños y desperdicio de agua.',
    image: '/images/fugas.jpg',
    icon: '01',
  },
  {
    title: 'Destape de drenajes',
    description:
      'Eliminamos obstrucciones en lavabos, tarjas, regaderas y tuberías con soluciones seguras.',
    image: '/images/destape.jpg',
    icon: '02',
  },
  {
    title: 'Reparación de tuberías',
    description:
      'Reparamos o reemplazamos tuberías dañadas, corroídas o con fugas para restaurar la presión.',
    image: '/images/tuberias.jpg',
    icon: '03',
  },
  {
    title: 'Instalación de muebles de baño',
    description:
      'Instalación profesional de lavabos, WC, regaderas, mezcladoras y accesorios de baño.',
    image: '/images/muebles.jpg',
    icon: '04',
  },
  {
    title: 'Tinacos y cisternas',
    description:
      'Mantenimiento y reparación para sistemas de almacenamiento de agua y presión doméstica.',
    image: '/images/tinacos.jpg',
    icon: '05',
  },
  {
    title: 'Calentadores',
    description:
      'Instalación, revisión y mantenimiento de calentadores para mayor eficiencia y seguridad.',
    image: '/images/calentador.png',
    icon: '06',
  },
  {
    title: 'Mantenimiento preventivo',
    description:
      'Revisamos tu instalación para detectar fallas antes de que se conviertan en gastos mayores.',
    image: '/images/mantenimineto.jpg',
    icon: '07',
  },
  {
    title: 'Emergencias de plomería',
    description:
      'Atención rápida para fugas, drenajes colapsados, falta de agua y otros problemas urgentes.',
    image: '/images/emergencia.png',
    icon: '08',
  },
]

const benefits = [
  'Diagnóstico profesional',
  'Precios claros',
  'Trabajo limpio',
  'Atención rápida',
]

const processSteps = [
  { number: '01', title: 'Cuéntanos qué sucede', description: 'Habla con nosotros y describe el problema o la emergencia.' },
  { number: '02', title: 'Evaluamos el problema', description: 'Revisamos la causa raíz y te orientamos con claridad.' },
  { number: '03', title: 'Te damos una cotización', description: 'Te presentamos una propuesta honesta antes de iniciar.' },
  { number: '04', title: 'Realizamos el trabajo', description: 'Ejecutamos la solución con calidad, limpieza y garantía.' },
]

const serviceAreas = ['Zona 1', 'Zona 2', 'Zona 3', 'Zona 4']

const faqs = [
  {
    question: '¿Cuánto cuesta una reparación de plomería?',
    answer:
      'El costo depende del tipo de problema, la complejidad del trabajo y los materiales requeridos. Te damos una cotización clara antes de iniciar.',
  },
  {
    question: '¿Realizan visitas a domicilio?',
    answer:
      'Sí. Realizamos atención a domicilio para servicios residenciales, comerciales y emergencias en nuestra zona de servicio.',
  },
  {
    question: '¿Atienden emergencias?',
    answer:
      'Sí. Contamos con atención para situaciones urgentes como fugas, drenajes bloqueados y falta de agua.',
  },
  {
    question: '¿Pueden reparar fugas ocultas?',
    answer:
      'Sí. Detectamos fugas visibles y ocultas para proteger tu hogar o negocio y evitar daños mayores.',
  },
  {
    question: '¿Instalan calentadores?',
    answer:
      'Sí. Realizamos instalación, revisión y mantenimiento de calentadores para asegurar su correcto funcionamiento.',
  },
  {
    question: '¿Trabajan con negocios?',
    answer:
      'Sí. Atendemos también propiedades comerciales y espacios con necesidades de mantenimiento y respuesta ágil.',
  },
]

const whatsappLink = `https://wa.me/${WHATSAPP_NUMBER}?text=${encodeURIComponent('Hola, necesito ayuda con un problema de plomería.')}`
const callLink = `tel:${PHONE_NUMBER.replace(/\s+/g, '')}`

const openFaq = ref<number | null>(0)
const isMenuOpen = ref(false)
const selectedService = ref<number | null>(null)
const isCommentFormOpen = ref(false)
const commentName = ref('')
const commentText = ref('')
const activeService = computed(() => selectedService.value === null ? null : services[selectedService.value])
const commentLink = computed(() => {
  const message = `Hola, quiero dejar un comentario sobre Plomería Aguilar.\nNombre: ${commentName.value}\nComentario: ${commentText.value}`
  return `https://wa.me/${WHATSAPP_NUMBER}?text=${encodeURIComponent(message)}`
})

const toggleFaq = (index: number) => {
  openFaq.value = openFaq.value === index ? null : index
}

const closeMenu = () => {
  isMenuOpen.value = false
}

const showService = (index: number) => {
  selectedService.value = index
  window.scrollTo({ top: 0, behavior: 'smooth' })
}

const closeService = () => {
  selectedService.value = null
  window.scrollTo({ top: 0, behavior: 'smooth' })
}

const closeCommentForm = () => {
  isCommentFormOpen.value = false
  commentName.value = ''
  commentText.value = ''
}
</script>

<template>
  <div class="page-shell">
    <header class="topbar">
      <nav class="navbar container" aria-label="Navegación principal">
        <a class="brand" href="#inicio" aria-label="Inicio de Plomería Aguilar">
          <img class="brand-logo" src="/images/logo.png" alt="Plomería Aguilar" />
        </a>

        <button
          class="menu-toggle"
          type="button"
          aria-label="Abrir menú"
          aria-expanded="false"
          :class="{ active: isMenuOpen }"
          @click="isMenuOpen = !isMenuOpen"
        >
          <span></span>
          <span></span>
          <span></span>
        </button>

        <div class="nav-links" :class="{ open: isMenuOpen }">
          <a href="#inicio" @click="closeMenu">Inicio</a>
          <a href="#servicios" @click="closeMenu">Servicios</a>
          <a href="#nosotros" @click="closeMenu">Nosotros</a>
          <a href="#proceso" @click="closeMenu">Proceso</a>
          <a href="#zonas" @click="closeMenu">Zonas de servicio</a>
          <a href="#faq" @click="closeMenu">FAQ</a>
          <a href="#contacto" @click="closeMenu">Contacto</a>
        </div>

        <a class="phone-pill desktop-only" :href="callLink" aria-label="Llamar ahora">
          <span class="phone-icon">TEL</span>
          <span>{{ PHONE_NUMBER }}</span>
        </a>

        <a class="whatsapp-cta desktop-only" :href="whatsappLink" target="_blank" rel="noopener noreferrer">
          WhatsApp
        </a>
      </nav>
    </header>

    <main id="inicio">
      <template v-if="selectedService === null">
      <section class="hero">
        <div class="container hero-grid">
          <div class="hero-copy">
            <div class="eyebrow">Plomería Aguilar • Servicio profesional</div>

            <h1>
              ¿Tienes una fuga?<br />
              Nosotros la solucionamos.<br />
              <span>rápido y sin complicaciones.</span>
            </h1>

            <p>
              Servicios de plomería residencial y comercial, reparaciones, instalaciones y atención de 
              emergencias. Soluciones profesionales para tu hogar o negocio.
            </p>

            <div class="cta-row">
              <a class="btn btn-primary" :href="whatsappLink" target="_blank" rel="noopener noreferrer">
                <span class="btn-icon">↗</span>
                Solicitar por WhatsApp
              </a>
              <a class="btn btn-secondary" :href="callLink">
                <span class="btn-icon">TEL</span>
                Llamar ahora
              </a>
            </div>

            <ul class="trust-list" aria-label="Beneficios principales">
              <li>✓ Atención rápida</li>
              <li>✓ Cotización clara</li>
              <li>✓ Trabajo profesional</li>
              <li>✓ Atención a emergencias</li>
            </ul>
          </div>

          <div class="hero-visual">
            <div class="image-card">
              <img
                src="/images/fugas.jpg"
                alt="Tubería con una fuga de agua"
              />
            </div>
            <div class="floating-badges" aria-label="Calificaciones y servicios">
              <span>Servicio confiable</span>
              <span>Respuesta rápida</span>
              <span>✓ Trabajo garantizado</span>
            </div>
          </div>
        </div>
      </section>

      <section class="stats-band" aria-label="Estadísticas de confianza">
        <div class="container stats-grid">
          <div v-for="(stat, index) in stats" :key="index" class="stat-card">
            <strong>{{ stat.value }}</strong>
            <span>{{ stat.label }}</span>
          </div>
        </div>
      </section>

      <section id="servicios" class="section services-section">
        <div class="container">
          <div class="section-heading">
            <span class="kicker">Servicios</span>
            <h2>Soluciones para cada problema de plomería</h2>
            <p>Desde una pequeña fuga hasta una emergencia, tenemos una solución para ti.</p>
          </div>

          <div class="services-grid">
            <article v-for="(service, index) in services" :key="index" class="service-card">
              <div class="service-image-wrap">
                <img :src="service.image" :alt="service.title" />
                <span class="service-icon">{{ service.icon }}</span>
              </div>
              <div class="service-body">
                <h3>{{ service.title }}</h3>
                <p>{{ service.description }}</p>
                <a href="#servicio-detalle" @click.prevent="showService(index)">Ver servicio <span>→</span></a>
              </div>
            </article>
          </div>
        </div>
      </section>

      <section id="nosotros" class="section why-us">
        <div class="container why-grid">
          <div class="why-image-wrap">
            <img
              src="/images/mantenimineto.jpg"
              alt="Profesional realizando un trabajo de plomería"
            />
          </div>

          <div class="why-copy">
            <span class="kicker">¿Por qué elegirnos?</span>
            <h2>Más que reparar tuberías, cuidamos tu hogar.</h2>
            <ul class="check-list">
              <li v-for="(benefit, index) in benefits" :key="index">✓ {{ benefit }}</li>
            </ul>
            <p>
              En Plomería Aguilar ofrecemos soluciones confiables, limpias y duraderas para hogares,
              negocios y propiedades. Nuestro enfoque combina experiencia técnica, atención cercana y
              respuesta rápida cuando más importa.
            </p>
          </div>
        </div>
      </section>

      <section id="proceso" class="section process-section">
        <div class="container">
          <div class="section-heading align-center">
            <span class="kicker">Proceso</span>
            <h2>Así de fácil resolvemos tu problema</h2>
          </div>

          <div class="process-grid">
            <div v-for="(step, index) in processSteps" :key="index" class="step-card">
              <div class="step-number">{{ step.number }}</div>
              <h3>{{ step.title }}</h3>
              <p>{{ step.description }}</p>
            </div>
          </div>
        </div>
      </section>

      <section class="section emergency-section">
        <div class="container emergency-box">
          <div>
            <span class="kicker light">Emergencias</span>
            <h2>¿Tienes una emergencia de plomería?</h2>
            <p>Una fuga no puede esperar. Contáctanos y recibe atención lo antes posible.</p>
            <div class="emergency-meta">Atención de emergencias</div>
          </div>
          <a class="btn btn-whatsapp" :href="whatsappLink" target="_blank" rel="noopener noreferrer">
            <span class="btn-icon">↗</span>
            Hablar por WhatsApp
          </a>
        </div>
      </section>

      <section class="section comment-section" id="comentarios">
        <div class="container">
          <div class="section-heading align-center">
            <span class="kicker">Tu experiencia</span>
            <h2>¿Ya trabajamos contigo?</h2>
            <p>Por ahora no mostramos comentarios públicos. Puedes enviarnos el tuyo directamente.</p>
          </div>

          <div class="comment-action">
            <button class="btn comment-trigger" type="button" @click="isCommentFormOpen = !isCommentFormOpen">
              {{ isCommentFormOpen ? 'Cerrar formulario' : 'Dejar un comentario' }}
              <span>{{ isCommentFormOpen ? '−' : '↗' }}</span>
            </button>

            <form v-if="isCommentFormOpen" class="comment-form" @submit.prevent>
              <label>
                Tu nombre
                <input v-model="commentName" type="text" placeholder="Escribe tu nombre" required />
              </label>
              <label>
                Tu comentario
                <textarea v-model="commentText" rows="4" placeholder="Cuéntanos cómo fue tu experiencia" required></textarea>
              </label>
              <a
                class="btn btn-primary"
                :class="{ disabled: !commentName.trim() || !commentText.trim() }"
                :href="commentName.trim() && commentText.trim() ? commentLink : undefined"
                target="_blank"
                rel="noopener noreferrer"
                @click="!commentName.trim() || !commentText.trim() ? $event.preventDefault() : closeCommentForm()"
              >
                Enviar comentario por WhatsApp <span>↗</span>
              </a>
            </form>
          </div>
        </div>
      </section>

      <section id="zonas" class="section service-areas">
        <div class="container">
          <div class="section-heading align-center">
            <span class="kicker">Zonas de servicio</span>
            <h2>¿Dónde trabajamos?</h2>
            <p>Atendemos hogares, negocios y propiedades en nuestra zona de servicio.</p>
          </div>

          <div class="areas-grid">
            <div v-for="(area, index) in serviceAreas" :key="index" class="area-pill">{{ area }}</div>
          </div>

          <div class="coverage-action">
            <a class="btn btn-secondary" href="#contacto">Consultar cobertura</a>
          </div>
        </div>
      </section>

      <section id="faq" class="section faq-section">
        <div class="container faq-wrap">
          <div class="section-heading align-center">
            <span class="kicker">FAQ</span>
            <h2>Preguntas frecuentes</h2>
          </div>

          <div class="faq-list" role="list">
            <div v-for="(item, index) in faqs" :key="index" class="faq-item" :class="{ open: openFaq === index }">
              <button type="button" class="faq-question" @click="toggleFaq(index)" :aria-expanded="openFaq === index">
                <span>{{ item.question }}</span>
                <span class="faq-plus">{{ openFaq === index ? '−' : '+' }}</span>
              </button>
              <div v-show="openFaq === index" class="faq-answer">
                <p>{{ item.answer }}</p>
              </div>
            </div>
          </div>
        </div>
      </section>

      <section class="section conversion-section" id="contacto">
        <div class="container conversion-box">
          <div>
            <span class="kicker">Contacto</span>
            <h2>¿Tienes un problema de plomería?</h2>
            <p>No lo dejes para después. Cuéntanos qué sucede y encontraremos la mejor solución.</p>
          </div>
          <div class="cta-row two-buttons">
            <a class="btn btn-primary" :href="whatsappLink" target="_blank" rel="noopener noreferrer">
              <span class="btn-icon">↗</span>
              Solicitar por WhatsApp
            </a>
            <a class="btn btn-secondary" :href="callLink">
              <span class="btn-icon">TEL</span>
              Llamar ahora
            </a>
          </div>
        </div>
      </section>
      </template>

      <section v-else class="service-detail-page" aria-labelledby="service-detail-title">
        <div class="container service-detail-wrap">
          <button class="service-back" type="button" @click="closeService">
            <span>←</span> Servicios <span class="service-back-separator">/</span>
            {{ activeService?.title }}
          </button>

          <div class="service-detail-grid">
            <div class="service-detail-copy">
              <span class="kicker">Servicio especializado</span>
              <h1 id="service-detail-title">{{ activeService?.title }}<br /><span>en Puebla</span></h1>
              <p class="service-detail-lead">
                Una atención oportuna evita daños mayores. Revisamos tu instalación, encontramos el origen
                del problema y proponemos una solución clara para tu hogar o negocio.
              </p>
              <p>
                En Plomería Aguilar trabajamos con el mínimo necesario para resolver el problema de forma
                limpia y duradera. Te explicamos cada paso y te damos una cotización antes de comenzar.
              </p>

              <div class="service-detail-actions">
                <a class="btn btn-primary" :href="whatsappLink" target="_blank" rel="noopener noreferrer">
                  <span class="btn-icon">↗</span>
                  Solicitar por WhatsApp
                </a>
                <a class="btn service-detail-call" :href="callLink">
                  <span class="btn-icon">TEL</span>
                  Llamar ahora
                </a>
              </div>
            </div>

            <div class="service-detail-image">
              <img :src="activeService?.image" :alt="activeService?.title" />
            </div>
          </div>
        </div>
      </section>
    </main>

    <footer class="site-footer">
      <div class="container footer-grid">
        <div class="footer-brand">
          <div class="brand footer-brand-mark">
            <img class="brand-logo" src="/images/logo2.png" alt="Plomería Aguilar" />
          </div>
          <p>Soluciones profesionales de plomería para hogares y negocios.</p>
        </div>

        <div>
          <h3>Servicios</h3>
          <ul>
            <li>Reparación de fugas</li>
            <li>Destape de drenajes</li>
            <li>Reparación de tuberías</li>
            <li>Instalaciones</li>
            <li>Calentadores</li>
          </ul>
        </div>

        <div>
          <h3>Empresa</h3>
          <ul>
            <li>Nosotros</li>
            <li>Servicios</li>
            <li>Zonas de servicio</li>
            <li>Contacto</li>
          </ul>
        </div>

        <div>
          <h3>Contacto</h3>
          <ul>
            <li>Teléfono: {{ PHONE_NUMBER }}</li>
            <li>WhatsApp: {{ WHATSAPP_NUMBER }}</li>
            <li>Horario: Lunes a domingo</li>
            <li>Ubicación: Zona de servicio</li>
          </ul>
        </div>
      </div>

      <div class="footer-bottom">
        <div class="container">© 2026 Plomería Aguilar. Todos los derechos reservados.</div>
      </div>
    </footer>

    <a class="floating-whatsapp" :href="whatsappLink" target="_blank" rel="noopener noreferrer" aria-label="Contactar por WhatsApp">
      <span class="floating-text">WhatsApp</span>
      <span class="floating-icon">↗</span>
    </a>
  </div>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600;700&family=Space+Grotesk:wght@500;600;700&display=swap');

:global(:root) {
  --ink: #102b2d;
  --ink-soft: #486366;
  --paper: #f4f1eb;
  --paper-deep: #e9e5dc;
  --white: #fffdf9;
  --petrol: #123c3d;
  --petrol-light: #1d5958;
  --copper: #c9784d;
  --line: rgba(16, 43, 45, 0.14);
}

:global(html) { scroll-behavior: smooth; }
:global(*) { box-sizing: border-box; }
:global(body) { margin: 0; background: var(--paper); color: var(--ink); font-family: 'DM Sans', sans-serif; }
:global(a) { text-decoration: none; }
:global(img) { display: block; max-width: 100%; }

.page-shell { min-height: 100vh; overflow: hidden; background: var(--paper); }
.container { width: min(1160px, calc(100% - 48px)); margin: 0 auto; }
.topbar { position: sticky; top: 0; z-index: 30; background: rgba(244, 241, 235, 0.9); border-bottom: 1px solid var(--line); backdrop-filter: blur(16px); }
.navbar { display: flex; align-items: center; justify-content: space-between; min-height: 76px; gap: 24px; }
.brand { display: inline-flex; align-items: center; gap: 11px; color: var(--ink); }
.brand-logo { width: 154px; height: 48px; object-fit: contain; object-position: left center; }
.brand-text { display: flex; flex-direction: column; line-height: 1; }
.brand-text strong { font-family: 'Space Grotesk', sans-serif; font-size: 0.93rem; letter-spacing: 0.05em; text-transform: uppercase; }
.brand-text small { margin-top: 5px; color: var(--ink-soft); font-size: 0.64rem; letter-spacing: 0.16em; text-transform: uppercase; }
.nav-links { display: flex; align-items: center; justify-content: center; gap: 25px; flex: 1; }
.nav-links a { color: var(--ink-soft); font-size: 0.83rem; font-weight: 600; transition: color 0.2s ease; }
.nav-links a:hover, .nav-links a:focus-visible { color: var(--copper); }
.phone-pill, .whatsapp-cta, .btn { display: inline-flex; align-items: center; justify-content: center; gap: 9px; font-weight: 700; transition: transform 0.2s ease, background 0.2s ease, box-shadow 0.2s ease; }
.phone-pill { padding: 0.72rem 0.86rem; border: 1px solid var(--line); color: var(--ink); font-size: 0.82rem; }
.phone-icon, .btn-icon { color: var(--copper); font-size: 0.9rem; }
.whatsapp-cta { padding: 0.78rem 1rem; background: var(--petrol); color: var(--white); font-size: 0.82rem; }
.desktop-only { display: inline-flex; }
.menu-toggle { display: none; width: 42px; height: 42px; border: 1px solid var(--line); background: transparent; cursor: pointer; }
.menu-toggle span { display: block; width: 18px; height: 1px; margin: 4px auto; background: var(--ink); }
.hero { position: relative; padding: 82px 0 72px; background: var(--petrol); color: var(--white); }
.hero::after { position: absolute; right: -10%; bottom: -35%; width: 55vw; height: 55vw; border: 1px solid rgba(255, 253, 249, 0.12); border-radius: 50%; content: ''; }
.hero-grid { position: relative; z-index: 1; display: grid; grid-template-columns: 1fr 0.84fr; align-items: center; gap: 80px; }
.eyebrow { display: inline-flex; align-items: center; gap: 10px; margin-bottom: 25px; color: #e5b294; font-size: 0.75rem; font-weight: 700; letter-spacing: 0.14em; text-transform: uppercase; }
.eyebrow::before { width: 26px; height: 1px; background: var(--copper); content: ''; }
.hero-copy h1 { max-width: 690px; margin: 0; font-family: 'Space Grotesk', sans-serif; font-size: clamp(3rem, 5.8vw, 6.1rem); line-height: 0.94; letter-spacing: -0.06em; }
.hero-copy h1 span { display: inline-block; color: #e5b294; }
.hero-copy p { max-width: 555px; margin: 28px 0 0; color: rgba(255, 253, 249, 0.72); font-size: 1.02rem; line-height: 1.75; }
.cta-row { display: flex; flex-wrap: wrap; gap: 12px; margin-top: 32px; }
.btn { min-height: 52px; padding: 0 1.3rem; border: 1px solid transparent; font-size: 0.9rem; }
.btn:hover, .whatsapp-cta:hover, .phone-pill:hover, .floating-whatsapp:hover { transform: translateY(-2px); }
.btn-primary, .btn-whatsapp { background: var(--copper); color: var(--white); box-shadow: 0 14px 30px rgba(201, 120, 77, 0.22); }
.btn-secondary { border-color: rgba(255, 253, 249, 0.3); background: transparent; color: var(--white); }
.trust-list { display: flex; flex-wrap: wrap; gap: 14px 25px; margin: 28px 0 0; padding: 0; color: rgba(255, 253, 249, 0.68); font-size: 0.82rem; list-style: none; }
.trust-list li::first-letter { color: var(--copper); }
.trust-list li { white-space: nowrap; }
.hero-visual { position: relative; display: flex; justify-content: flex-end; }
.image-card { width: min(100%, 485px); border: 1px solid rgba(255, 253, 249, 0.2); border-radius: 2px; overflow: hidden; box-shadow: 26px 26px 0 rgba(201, 120, 77, 0.28); }
.image-card img { width: 100%; height: 555px; object-fit: cover; filter: saturate(0.78); }
.floating-badges { position: absolute; right: -24px; bottom: 22px; display: grid; gap: 7px; }
.floating-badges span { padding: 0.65rem 0.8rem; border-left: 2px solid var(--copper); background: rgba(16, 43, 45, 0.84); color: var(--white); font-size: 0.72rem; letter-spacing: 0.03em; }
.stats-band { padding: 0; background: var(--paper-deep); }
.stats-grid { display: grid; grid-template-columns: repeat(4, 1fr); border-left: 1px solid var(--line); }
.stat-card { min-height: 124px; padding: 26px 22px; border-right: 1px solid var(--line); }
.stat-card strong { display: block; color: var(--petrol); font-family: 'Space Grotesk', sans-serif; font-size: clamp(2rem, 3vw, 3.2rem); line-height: 1; letter-spacing: -0.06em; }
.stat-card span { display: block; margin-top: 10px; color: var(--ink-soft); font-size: 0.79rem; }
.section { padding: 112px 0; }
.section-heading { max-width: 720px; margin-bottom: 43px; }
.kicker { display: inline-block; margin-bottom: 13px; color: var(--copper); font-size: 0.72rem; font-weight: 700; letter-spacing: 0.18em; text-transform: uppercase; }
.kicker.light { color: #e5b294; }
.section-heading h2, .why-copy h2, .emergency-box h2, .conversion-box h2 { margin: 0; font-family: 'Space Grotesk', sans-serif; font-size: clamp(2.3rem, 4.2vw, 4.4rem); line-height: 0.98; letter-spacing: -0.06em; }
.section-heading p { max-width: 570px; margin: 20px 0 0; color: var(--ink-soft); font-size: 1rem; line-height: 1.75; }
.services-section { background: var(--white); }
.services-grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: 1px; background: var(--line); border: 1px solid var(--line); }
.service-card { background: var(--white); transition: background 0.25s ease; }
.service-card:hover { background: #f0ece4; }
.service-image-wrap { position: relative; height: 190px; overflow: hidden; }
.service-image-wrap img { width: 100%; height: 100%; object-fit: cover; filter: saturate(0.72); transition: transform 0.35s ease; }
.service-card:hover .service-image-wrap img { transform: scale(1.04); }
.service-icon { position: absolute; right: 14px; bottom: 14px; display: grid; place-items: center; width: 38px; height: 38px; border: 1px solid rgba(255, 253, 249, 0.45); background: var(--petrol); color: #e5b294; font-family: 'Space Grotesk', sans-serif; font-size: 0.8rem; font-weight: 700; }
.service-body { padding: 22px 18px 23px; }
.service-body h3 { margin: 0 0 10px; font-family: 'Space Grotesk', sans-serif; font-size: 1.17rem; letter-spacing: -0.04em; }
.service-body p { min-height: 82px; margin: 0; color: var(--ink-soft); font-size: 0.85rem; line-height: 1.65; }
.service-body a { display: inline-flex; gap: 8px; margin-top: 17px; color: var(--copper); font-size: 0.82rem; font-weight: 700; }
.service-detail-page { min-height: calc(100vh - 76px); padding: 54px 0 90px; background: var(--white); }
.service-detail-wrap { max-width: 1280px; }
.service-back { display: inline-flex; align-items: center; gap: 10px; margin: 0 0 56px; padding: 0; border: 0; background: transparent; color: #1764be; font: inherit; font-size: 0.88rem; cursor: pointer; }
.service-back > span:first-child { font-size: 1.2rem; }
.service-back-separator { color: #8293aa; }
.service-detail-grid { display: grid; grid-template-columns: 1fr 0.86fr; align-items: center; gap: 82px; }
.service-detail-copy h1 { margin: 0; color: #161e2e; font-family: 'Space Grotesk', sans-serif; font-size: clamp(3.2rem, 5.2vw, 5.2rem); line-height: 0.98; letter-spacing: -0.07em; }
.service-detail-copy h1 span { color: var(--petrol); }
.service-detail-copy p { max-width: 680px; margin: 24px 0 0; color: #58718f; font-size: 1.1rem; line-height: 1.85; }
.service-detail-copy .service-detail-lead { margin-top: 26px; }
.service-detail-actions { display: flex; flex-wrap: wrap; gap: 16px; margin-top: 28px; }
.service-detail-call { border-color: var(--petrol); background: var(--petrol); color: var(--white); box-shadow: 0 14px 30px rgba(18, 60, 61, 0.2); }
.service-detail-call .btn-icon { color: #e5b294; }
.service-detail-call:hover { background: var(--petrol-light); }
.service-detail-image { overflow: hidden; border-radius: 24px; box-shadow: 0 18px 44px rgba(16, 43, 45, 0.12); }
.service-detail-image img { width: 100%; height: 365px; object-fit: cover; filter: saturate(0.78); }
.why-us { background: var(--paper-deep); }
.why-grid { display: grid; grid-template-columns: 0.9fr 1fr; align-items: center; gap: 82px; }
.why-image-wrap { overflow: hidden; border: 1px solid var(--line); box-shadow: 18px 18px 0 var(--copper); }
.why-image-wrap img { width: 100%; height: 600px; object-fit: cover; filter: saturate(0.74); }
.why-copy h2 { max-width: 550px; }
.check-list { display: grid; grid-template-columns: repeat(2, 1fr); gap: 14px 18px; margin: 32px 0 27px; padding: 0; color: var(--petrol); font-size: 0.9rem; font-weight: 700; list-style: none; }
.check-list li { display: flex; align-items: center; gap: 10px; }
.why-copy p { max-width: 540px; margin: 0; color: var(--ink-soft); font-size: 0.98rem; line-height: 1.8; }
.process-section, .service-areas { background: var(--white); }
.align-center { margin-right: auto; margin-left: auto; text-align: center; }
.align-center p { margin-right: auto; margin-left: auto; }
.process-grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: 30px; }
.step-card { padding: 0 20px 0 0; border-right: 1px solid var(--line); }
.step-card:last-child { border-right: 0; }
.step-number { display: block; margin-bottom: 24px; color: var(--copper); font-family: 'Space Grotesk', sans-serif; font-size: 1.1rem; font-weight: 700; }
.step-card h3 { margin: 0 0 12px; font-family: 'Space Grotesk', sans-serif; font-size: 1.23rem; letter-spacing: -0.04em; }
.step-card p { margin: 0; color: var(--ink-soft); font-size: 0.88rem; line-height: 1.7; }
.emergency-section { background: var(--petrol); color: var(--white); }
.emergency-box { display: flex; align-items: center; justify-content: space-between; gap: 36px; }
.emergency-box h2 { max-width: 610px; }
.emergency-box p { max-width: 570px; margin: 18px 0 12px; color: rgba(255, 253, 249, 0.7); line-height: 1.7; }
.emergency-meta { display: inline-block; color: #e5b294; font-size: 0.78rem; font-weight: 700; letter-spacing: 0.08em; text-transform: uppercase; }
.testimonials-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 1px; background: var(--line); border: 1px solid var(--line); }
.testimonial-card { min-height: 240px; padding: 28px 25px; background: var(--white); }
.avatar { display: grid; place-items: center; width: 40px; height: 40px; margin-bottom: 24px; background: var(--copper); color: var(--white); font-family: 'Space Grotesk', sans-serif; font-weight: 700; }
.testimonial-header { display: flex; align-items: center; justify-content: space-between; gap: 12px; margin-bottom: 13px; }
.testimonial-header h3 { margin: 0; font-family: 'Space Grotesk', sans-serif; font-size: 1rem; }
.stars { color: var(--copper); font-size: 0.8rem; letter-spacing: 0.12em; }
.testimonial-card p { margin: 0; color: var(--ink-soft); font-size: 0.9rem; line-height: 1.75; }
.comment-section { background: var(--paper-deep); }
.comment-action { display: grid; justify-items: center; }
.comment-trigger { border: 1px solid var(--petrol); background: transparent; color: var(--petrol); }
.comment-trigger:hover { background: var(--petrol); color: var(--white); }
.comment-trigger span { color: var(--copper); font-size: 1rem; }
.comment-form { display: grid; gap: 18px; width: min(100%, 620px); margin-top: 24px; padding: 28px; border: 1px solid var(--line); background: var(--white); }
.comment-form label { display: grid; gap: 8px; color: var(--petrol); font-size: 0.8rem; font-weight: 700; }
.comment-form input, .comment-form textarea { width: 100%; padding: 13px 14px; border: 1px solid var(--line); border-radius: 0; background: var(--paper); color: var(--ink); font: inherit; font-size: 0.9rem; resize: vertical; }
.comment-form input:focus, .comment-form textarea:focus { outline: 2px solid rgba(201, 120, 77, 0.35); border-color: var(--copper); }
.comment-form .btn { width: fit-content; }
.comment-form .disabled { cursor: not-allowed; opacity: 0.45; }
.areas-grid { display: grid; grid-template-columns: repeat(4, 1fr); border-top: 1px solid var(--line); border-left: 1px solid var(--line); }
.area-pill { padding: 25px 16px; border-right: 1px solid var(--line); border-bottom: 1px solid var(--line); color: var(--petrol); font-family: 'Space Grotesk', sans-serif; font-size: 1rem; font-weight: 600; text-align: center; }
.coverage-action { display: flex; justify-content: center; margin-top: 29px; }
.faq-wrap { max-width: 850px; margin: 0 auto; }
.faq-list { display: grid; gap: 0; border-top: 1px solid var(--line); }
.faq-item { border-bottom: 1px solid var(--line); }
.faq-question { display: flex; align-items: center; justify-content: space-between; width: 100%; gap: 16px; padding: 20px 0; border: 0; background: transparent; color: var(--ink); font-family: 'DM Sans', sans-serif; font-size: 0.98rem; font-weight: 700; text-align: left; cursor: pointer; }
.faq-plus { color: var(--copper); font-family: 'Space Grotesk', sans-serif; font-size: 1.5rem; font-weight: 400; }
.faq-answer { padding: 0 40px 19px 0; }
.faq-answer p { margin: 0; color: var(--ink-soft); font-size: 0.9rem; line-height: 1.75; }
.conversion-section { padding-top: 0; padding-bottom: 110px; background: var(--white); }
.conversion-box { display: flex; align-items: center; justify-content: space-between; gap: 28px; padding: 48px; background: var(--paper-deep); border-top: 3px solid var(--copper); }
.conversion-box h2 { max-width: 610px; color: var(--petrol); }
.conversion-box p { max-width: 600px; margin: 16px 0 0; color: var(--ink-soft); line-height: 1.7; }
.conversion-box .btn-secondary { color: var(--ink); }
.two-buttons { justify-content: flex-end; }
.site-footer { padding-top: 55px; background: var(--petrol); color: var(--white); }
.footer-grid { display: grid; grid-template-columns: 1.4fr 1fr 1fr 1.1fr; gap: 40px; padding-bottom: 40px; }
.footer-brand-mark { margin-bottom: 16px; }
.footer-brand-mark .brand-logo { width: 230px; height: 72px; object-position: left center; }
.footer-brand p, .footer-grid li { color: rgba(255, 253, 249, 0.64); font-size: 0.86rem; line-height: 1.9; }
.footer-grid h3 { margin: 0 0 18px; color: #e5b294; font-size: 0.72rem; letter-spacing: 0.15em; text-transform: uppercase; }
.footer-grid ul { margin: 0; padding: 0; list-style: none; }
.footer-bottom { padding: 18px 0 25px; border-top: 1px solid rgba(255, 253, 249, 0.15); color: rgba(255, 253, 249, 0.5); font-size: 0.76rem; }
.floating-whatsapp { position: fixed; right: 22px; bottom: 22px; z-index: 50; display: inline-flex; align-items: center; gap: 9px; padding: 0.78rem 1rem; background: var(--copper); color: var(--white); box-shadow: 0 16px 32px rgba(201, 120, 77, 0.3); transition: transform 0.2s ease, box-shadow 0.2s ease; }
.floating-icon { font-size: 0.9rem; }
.floating-text { font-size: 0.78rem; font-weight: 700; }

@media (max-width: 1024px) {
  .nav-links { gap: 14px; }
  .hero-grid { gap: 40px; }
  .services-grid { grid-template-columns: repeat(2, 1fr); }
  .process-grid { grid-template-columns: repeat(2, 1fr); gap: 35px 30px; }
  .step-card:nth-child(2) { border-right: 0; }
  .footer-grid { grid-template-columns: repeat(2, 1fr); }
}

@media (max-width: 820px) {
  .container { width: min(100% - 32px, 620px); }
  .nav-links { position: absolute; top: 76px; left: 16px; right: 16px; display: none; flex-direction: column; gap: 17px; align-items: flex-start; padding: 20px; background: var(--white); border: 1px solid var(--line); box-shadow: 0 18px 35px rgba(16, 43, 45, 0.12); }
  .nav-links.open { display: flex; }
  .menu-toggle { display: block; }
  .desktop-only { display: none; }
  .brand-logo { width: 138px; height: 44px; }
  .hero { padding: 62px 0 60px; }
  .hero-grid, .why-grid { grid-template-columns: 1fr; gap: 48px; }
  .service-detail-grid { grid-template-columns: 1fr; gap: 38px; }
  .service-detail-page { padding-top: 35px; }
  .service-back { margin-bottom: 38px; }
  .service-detail-copy h1 { font-size: clamp(2.8rem, 13vw, 4.4rem); }
  .service-detail-copy p { font-size: 0.96rem; }
  .service-detail-actions { flex-direction: column; align-items: stretch; }
  .service-detail-image { order: -1; }
  .service-detail-image img { height: 280px; }
  .hero-copy h1 { font-size: clamp(3rem, 14vw, 5rem); }
  .hero-copy p { font-size: 0.94rem; }
  .hero-visual { justify-content: center; }
  .image-card { width: calc(100% - 16px); box-shadow: 14px 14px 0 rgba(201, 120, 77, 0.28); }
  .image-card img { height: 420px; }
  .floating-badges { right: 0; }
  .stats-grid, .areas-grid { grid-template-columns: repeat(2, 1fr); }
  .stat-card { min-height: 105px; padding: 20px 14px; }
  .section { padding: 78px 0; }
  .section-heading h2, .why-copy h2, .emergency-box h2, .conversion-box h2 { font-size: clamp(2.4rem, 11vw, 4rem); }
  .why-image-wrap img { height: 440px; }
  .check-list { grid-template-columns: 1fr; }
  .conversion-box, .emergency-box { display: grid; align-items: start; padding: 32px 24px; }
  .two-buttons { justify-content: stretch; }
  .cta-row { flex-direction: column; align-items: stretch; }
  .btn { width: 100%; }
  .floating-whatsapp { right: 16px; bottom: 16px; width: 48px; height: 48px; justify-content: center; padding: 0; }
  .floating-text { display: none; }
}

@media (max-width: 560px) {
  .services-grid, .process-grid, .footer-grid { grid-template-columns: 1fr; }
  .step-card, .step-card:nth-child(2) { border-right: 0; border-bottom: 1px solid var(--line); padding: 0 0 25px; }
  .step-card:last-child { border-bottom: 0; }
  .service-body p { min-height: auto; }
  .process-grid { gap: 25px; }
}
</style>

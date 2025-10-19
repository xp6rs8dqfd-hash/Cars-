# Cars-
It’s about cars 
// أسماء الصور — غيّرها بحسب اسم ملفاتك
const slides = [
  {
    src: 'camry2018.jpg',
    title: 'تويوتا كامري - 2018',
    desc: 'محرك 4 سلندر — مثال توضيحي.',
    link: '#'
  },
  {
    src: 'lancer2005.jpg',
    title: 'ميتسوبيشي لنسر - 2005',
    desc: 'موديل 2005 — مواصفات تقريبية.',
    link: '#'
  }
];

let idx = 0;
const mainImage = document.getElementById('mainImage');
const titleEl = document.getElementById('title');
const descEl = document.getElementById('desc');
const moreLink = document.getElementById('moreLink');
const prevBtn = document.getElementById('prevBtn');
const nextBtn = document.getElementById('nextBtn');
const toggleBtn = document.getElementById('toggleBtn');

function render(){
  const s = slides[idx];
  mainImage.src = s.src;
  mainImage.alt = s.title;
  titleEl.textContent = s.title;
  descEl.textContent = s.desc;
  moreLink.href = s.link;
}

function next(){
  idx = (idx + 1) % slides.length;
  render();
}
function prev(){
  idx = (idx - 1 + slides.length) % slides.length;
  render();
}

nextBtn.addEventListener('click', next);
prevBtn.addEventListener('click', prev);
toggleBtn.addEventListener('click', next);

// تغيير بالصوت أو النقر على الصورة ممكن أيضًا:
mainImage.addEventListener('click', next);

// --- دعم تحريك الجهاز: إذا لَمسَ ميل الجهاز لليمين (>20) نبدل الصورة
if (window.DeviceOrientationEvent) {
  let lastSwitch = 0;
  window.addEventListener('deviceorientation', (ev) => {
    // gamma: قياس الميل يمين/يسار
    const gamma = ev.gamma || 0;
    const now = Date.now();
    // منع التبديل السريع المتكرر: مرة كل 700ms
    if (gamma > 20 && now - lastSwitch > 700) {
      next(); lastSwitch = now;
    } else if (gamma < -20 && now - lastSwitch > 700) {
      prev(); lastSwitch = now;
    }
  }, true);
}
render();

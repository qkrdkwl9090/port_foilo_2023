<script setup>
onMounted(() => {
  /*--------------------
Vars
--------------------*/
  let progress = 50
  let startX = 0
  let active = 0
  let isDown = false

  /*--------------------
Contants
--------------------*/
  const speedWheel = 0.02
  const speedDrag = -0.1

  /*--------------------
Get Z
--------------------*/
  const getZindex = (array, index) =>
    array.map((_, i) => (index === i ? array.length : array.length - Math.abs(index - i)))

  /*--------------------
Items
--------------------*/
  const $items = document.querySelectorAll('.carousel-item')
  const $cursors = document.querySelectorAll('.cursor')

  const displayItems = (item, index, active) => {
    const zIndex = getZindex([...$items], active)[index]
    item.style.setProperty('--zIndex', zIndex)
    item.style.setProperty('--active', (index - active) / $items.length)
  }

  /*--------------------
Animate
--------------------*/
  const animate = () => {
    progress = Math.max(0, Math.min(progress, 100))
    active = Math.floor((progress / 100) * ($items.length - 1))

    $items.forEach((item, index) => displayItems(item, index, active))
  }
  animate()

  /*--------------------
Click on Items
--------------------*/
  $items.forEach((item, i) => {
    item.addEventListener('click', () => {
      progress = (i / $items.length) * 100 + 10
      animate()
    })
  })

  /*--------------------
Handlers
--------------------*/
  const handleWheel = (e) => {
    const wheelProgress = e.deltaY * speedWheel
    progress = progress + wheelProgress
    animate()
  }

  const handleMouseMove = (e) => {
    if (e.type === 'mousemove') {
      $cursors.forEach(($cursor) => {
        $cursor.style.transform = `translate(${e.clientX}px, ${e.clientY}px)`
      })
    }
    if (!isDown) return
    const x = e.clientX || (e.touches && e.touches[0].clientX) || 0
    const mouseProgress = (x - startX) * speedDrag
    progress = progress + mouseProgress
    startX = x
    animate()
  }

  const handleMouseDown = (e) => {
    isDown = true
    startX = e.clientX || (e.touches && e.touches[0].clientX) || 0
  }

  const handleMouseUp = () => {
    isDown = false
  }

  /*--------------------
Listeners
--------------------*/
  document.addEventListener('mousewheel', handleWheel)
  document.addEventListener('mousedown', handleMouseDown)
  document.addEventListener('mousemove', handleMouseMove)
  document.addEventListener('mouseup', handleMouseUp)
  document.addEventListener('touchstart', handleMouseDown)
  document.addEventListener('touchmove', handleMouseMove)
  document.addEventListener('touchend', handleMouseUp)
})
</script>

<template>
  <div class="carousel">
    <div class="carousel-item">
      <div class="carousel-box">
        <div class="title">Paris</div>
        <div class="num">01</div>
        <img
          src="https://media.istockphoto.com/id/949299844/it/foto/vista-prospettica-dellesterno-delledificio-contemporaneo.jpg?s=612x612&w=0&k=20&c=_DR1aRHuTEV3EYBJo1ZXq1pF4SgwB9EVWQLaBj4sC5g="
        />
      </div>
    </div>

    <div class="carousel-item">
      <div class="carousel-box">
        <div class="title">Warsaw</div>
        <div class="num">02</div>
        <img
          src="https://media.istockphoto.com/id/1150545984/it/foto/palazzo-moderno-di-lusso-con-piscina.jpg?s=612x612&w=0&k=20&c=Pbrai_VGc9tUviMCF1UaBErdS1YGyIVWsD29jzMZwTY="
        />
      </div>
    </div>

    <div class="carousel-item">
      <div class="carousel-box">
        <div class="title">Madrid</div>
        <div class="num">03</div>
        <img
          src="https://media.istockphoto.com/id/1214351345/it/foto/guardando-direttamente-lo-skyline-del-quartiere-finanziario-nel-centro-di-londra-immagine-di.jpg?s=612x612&w=0&k=20&c=oNNbPzPvcQ-4RA6AeatNIxHQIafBiXmDRtUUY0Ska-I="
        />
      </div>
    </div>

    <div class="carousel-item">
      <div class="carousel-box">
        <div class="title">Sydney</div>
        <div class="num">04</div>
        <img
          src="https://media.istockphoto.com/id/904390980/it/foto/foto-di-architettura-contemporanea-astratta.jpg?s=612x612&w=0&k=20&c=_P4Wmx5nq5MeDuimpNklKCBlrLovmCyd9lfiMKeJZDs="
        />
      </div>
    </div>

    <div class="carousel-item">
      <div class="carousel-box">
        <div class="title">Istanbul</div>
        <div class="num">05</div>
        <img
          src="https://media.istockphoto.com/id/130408311/it/foto/piscina-allesterno-della-casa-moderna-al-crepuscolo.jpg?s=612x612&w=0&k=20&c=ZoVjx7uDjoHKmpM1ayW6UR1SQOoYh_xx-QMG_qeOYs0="
        />
      </div>
    </div>

    <div class="carousel-item">
      <div class="carousel-box">
        <div class="title">Prague</div>
        <div class="num">06</div>
        <img
          src="https://media.istockphoto.com/id/1299954175/it/foto/villa-cubica-moderna.jpg?s=612x612&w=0&k=20&c=DhGhb3c1E3DW_fbrWJ_R_Zh0Lbwu6syFeRLsKlZ9no8="
        />
      </div>
    </div>

    <div class="carousel-item">
      <div class="carousel-box">
        <div class="title">Munich</div>
        <div class="num">07</div>
        <img
          src="https://media.istockphoto.com/id/926689776/it/foto/vista-ad-angolo-basso-dei-grattacieli-di-new-york.jpg?s=612x612&w=0&k=20&c=DmEB0Ty7ZwDnBoU5SuA8FNevOp4G1UcECw5aS4vA9A8="
        />
      </div>
    </div>

    <div class="carousel-item">
      <div class="carousel-box">
        <div class="title">Venice</div>
        <div class="num">08</div>
        <img
          src="https://media.istockphoto.com/id/1191376167/it/foto/villa-dellisola.jpg?s=612x612&w=0&k=20&c=PKslWo4FdbjinohKQlK_oWL34jqAsnzMTdy2bxEAf-I="
        />
      </div>
    </div>

    <div class="carousel-item">
      <div class="carousel-box">
        <div class="title">Oslo</div>
        <div class="num">09</div>
        <img
          src="https://media.istockphoto.com/id/184316397/it/foto/londra-edifici-aziendali.jpg?s=612x612&w=0&k=20&c=XqrRxEPzFnwRFk7PQrCiu9-FPfCTPyMe5BKKaxYXCs8="
        />
      </div>
    </div>
    <div class="carousel-item">
      <div class="carousel-box">
        <div class="title">London</div>
        <div class="num">10</div>
        <img
          src="https://media.istockphoto.com/id/184619832/it/foto/distretto-finanziario-al-crepuscolo-londra.jpg?s=612x612&w=0&k=20&c=RAThrJOBY6vhlT6-kQpu9-9jLEzWToYfdw46S8B0Mu0="
        />
      </div>
    </div>
  </div>

  <div class="layout">
    <div class="box">
      High-end, full-service<br />visual content creation<br />for lifestyle branding.
    </div>
  </div>
  <div class="cursor"></div>
  <div class="cursor cursor2"></div>
</template>
<style>
.carousel {
  position: relative;
  z-index: 1;
  height: 100vh;
  overflow: hidden;
  pointer-events: none;
}

.carousel-item {
  --items: 10;
  --width: clamp(150px, 30vw, 300px);
  --height: clamp(200px, 40vw, 400px);
  --x: calc(var(--active) * 800%);
  --y: calc(var(--active) * 200%);
  --rot: calc(var(--active) * 120deg);
  --opacity: calc(var(--zIndex) / var(--items) * 3 - 2);
  overflow: hidden;
  position: absolute;
  z-index: var(--zIndex);
  width: var(--width);
  height: var(--height);
  margin: calc(var(--height) * -0.5) 0 0 calc(var(--width) * -0.5);
  border-radius: 10px;
  top: 50%;
  left: 50%;
  user-select: none;
  transform-origin: 0% 100%;
  box-shadow: 0 10px 50px 10px rgba(0, 0, 0, 0.5);
  background: black;
  pointer-events: all;
  transform: translate(var(--x), var(--y)) rotate(var(--rot));
  transition: transform 0.8s cubic-bezier(0, 0.02, 0, 1);

  .carousel-box {
    position: absolute;
    z-index: 1;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    transition: opacity 0.8s cubic-bezier(0, 0.02, 0, 1);
    opacity: var(--opacity);
    font-family: 'Orelo-sw-db', serif;

    &:before {
      content: '';
      position: absolute;
      z-index: 1;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: linear-gradient(
        to bottom,
        rgba(0, 0, 0, 0.3),
        rgba(0, 0, 0, 0) 30%,
        rgba(0, 0, 0, 0) 50%,
        rgba(0, 0, 0, 0.5)
      );
    }
  }

  .title {
    position: absolute;
    z-index: 1;
    color: #fff;
    bottom: 20px;
    left: 20px;
    transition: opacity 0.8s cubic-bezier(0, 0.02, 0, 1);
    font-size: clamp(20px, 3vw, 30px);
    text-shadow: 0 4px 4px rgba(0, 0, 0, 0.1);
  }

  .num {
    position: absolute;
    z-index: 1;
    color: #fff;
    top: 10px;
    left: 20px;
    transition: opacity 0.8s cubic-bezier(0, 0.02, 0, 1);
    font-size: clamp(20px, 10vw, 80px);
  }

  img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    pointer-events: none;
  }
}

.layout {
  position: absolute;
  z-index: 0;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;

  &:before {
    content: '';
    position: absolute;
    z-index: 1;
    top: 0;
    left: 90px;
    width: 10px;
    height: 100%;
    border: 1px solid #fff;
    border-top: none;
    border-bottom: none;
    opacity: 0.15;
  }

  .box {
    position: absolute;
    bottom: 0;
    left: 30px;
    color: #fff;
    transform-origin: 0% 10%;
    transform: rotate(-90deg);
    font-size: 9px;
    line-height: 1.4;
    text-transform: uppercase;
    opacity: 0.4;
  }
}

.logo {
  position: absolute;
  z-index: 2;
  top: 28px;
  right: 28px;
  width: 30px;
  height: 30px;
  background: #fff;
  border-radius: 50%;
  opacity: 0.5;
  display: flex;
  justify-content: center;
  align-items: center;
  font-family: 'Orelo-sw-db', serif;
  pointer-events: all;
  color: black;
  text-decoration: none;
  font-size: 20px;
  overflow: hidden;
  padding-bottom: 0.1em;
}

.social {
  position: absolute;
  z-index: 10;
  bottom: 20px;
  right: 25px;
  color: #fff;
  opacity: 0.4;

  a {
    display: inline-block;
    margin-left: 3px;
  }

  svg {
    --fill: #fff;
    width: 35px;
    height: 35px;
  }
}

.cursor {
  position: fixed;
  z-index: 10;
  top: 0;
  left: 0;
  --size: 40px;
  width: var(--size);
  height: var(--size);
  border-radius: 50%;
  border: 1px solid rgba(255, 255, 255, 0.2);
  margin: calc(var(--size) * -0.5) 0 0 calc(var(--size) * -0.5);
  transition: transform 0.85s cubic-bezier(0, 0.02, 0, 1);
  display: none;
  pointer-events: none;

  @media (pointer: fine) {
    display: block;
  }
}

.cursor2 {
  --size: 2px;
  transition-duration: 0.7s;
}
</style>

<style scoped>
canvas {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  z-index: -1; /* Esto lo pone detrás */
  background-color: white; /* El fondo del canvas es blanco */
}

/* IMPORTANTE que el body y main sean transparentes */
</style>
<template><canvas ref="fondoCanvas"></canvas></template>

<script setup>
import { useTemplateRef, onMounted, onUnmounted } from 'vue'

const canvas = useTemplateRef('fondoCanvas')

onMounted(() => {
  const ctx = canvas.value.getContext('2d')
  let triangulos = []
  let lastScrollY = window.scrollY
  let scrollVelocity = 0

  const CANTIDAD = 600
  const TAMANO_MAX = 15
  const COLOR_HEX = '#f8c52d'
  const VELOCIDAD_BASE = 0.15
  const SENSIBILIDAD_SCROLL = 3 // Controla qué tanto reaccionan al scroll

  class Triangulo {
    constructor() {
      this.init()
    }

    init() {
      this.x = Math.random() * window.innerWidth
      this.y = Math.random() * window.innerHeight
      this.size = Math.random() * TAMANO_MAX + 2
      this.velX = (Math.random() - 0.5) * VELOCIDAD_BASE
      this.velY = (Math.random() - 0.5) * VELOCIDAD_BASE
      this.alpha = 0.2 + Math.random() * 0.2
      this.frecuencia = Math.random() * 0.02
      // Factor individual para que unos se muevan más que otros (efecto profundidad)
      this.parallaxFactor = Math.random() * SENSIBILIDAD_SCROLL
    }

    actualizar(velocity) {
      this.x += this.velX
      // Sumamos la velocidad del scroll multiplicada por su factor de profundidad
      this.y += this.velY - velocity * this.parallaxFactor

      // Reposicionamiento infinito
      if (this.x < -10) this.x = canvas.value.width + 10
      if (this.x > canvas.value.width + 10) this.x = -10
      if (this.y < -20) this.y = canvas.height + 20
      if (this.y > canvas.height + 20) this.y = -20
    }

    dibujar() {
      let brillar = this.alpha + Math.sin(Date.now() * this.frecuencia) * 0.05
      ctx.save()
      ctx.globalAlpha = Math.max(0.02, brillar)
      ctx.fillStyle = COLOR_HEX
      ctx.beginPath()
      ctx.moveTo(this.x, this.y)
      ctx.lineTo(this.x + this.size, this.y)
      ctx.lineTo(this.x + this.size / 2, this.y - this.size * 0.86)
      ctx.closePath()
      ctx.fill()
      ctx.restore()
    }
  }

  const manejarScroll = () => {
    const currentScrollY = window.scrollY
    scrollVelocity = currentScrollY - lastScrollY
    lastScrollY = currentScrollY
  }

  function configurar() {
    canvas.value.width = window.innerWidth
    canvas.value.height = window.innerHeight
    triangulos = []
    for (let i = 0; i < CANTIDAD; i++) {
      triangulos.push(new Triangulo())
    }
  }

  function animar() {
    ctx.clearRect(0, 0, canvas.value.width, canvas.value.height)

    triangulos.forEach((t) => {
      t.actualizar(scrollVelocity)
      t.dibujar()
    })

    // Reducimos gradualmente la velocidad del scroll para un efecto suave (fricción)
    scrollVelocity *= 0.9

    requestAnimationFrame(animar)
  }

  window.addEventListener('resize', configurar)
  window.addEventListener('scroll', manejarScroll)

  configurar()
  animar()

  // Limpieza de eventos al destruir el componente
  onUnmounted(() => {
    window.removeEventListener('resize', configurar)
    window.removeEventListener('scroll', manejarScroll)
  })
})
</script>

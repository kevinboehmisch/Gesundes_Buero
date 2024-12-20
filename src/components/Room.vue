<script>
export default {
  name: "Room",
  props: {
    name: {
      type: String,
      default: "Büroraum",
    },
    image: {
      type: String,
      required: true
    },
    temperature: {
      type: [Number, String],
      required: true,
    },
    humidity: {
      type: [Number, String],
      required: true,
    },
    number: {
      type: [Number, String],
      required: true,
    },
    status: {
      type: Object,
      default: () => ({
        temp_status: 'unknown',
        humidity_status: 'unknown'
      })
    }
  },
  computed: {
    // Farbe basierend auf der Temperatur
    temperatureColor() {
      if (this.temperature < 20) return "#87cefa"; // Unter 20°C → Blau
      if (this.temperature > 24) return "#cd5c5c"; // Über 24°C → Rot
      return "#3cb371"; // Dazwischen → Grün
    },
    // Farbe basierend auf der Luftfeuchtigkeit
    humidityColor() {
      if (this.humidity < 45) return "#87cefa"; // Unter 30% → Blau
      if (this.humidity > 55) return "#cd5c5c"; // Über 60% → Rot
      return "#3cb371"; // Dazwischen → Grün
    },
  },
};
</script>

<template>
  <div class="room-card" @click="$emit('click')">
    <h2 class="room-title">{{ name }} {{ number }}</h2>
    <div class="room-layout">
      <img :src="image" alt="Raum Layout" class="room-image" />
      <div class="metrics">
        <!-- Dynamische Farbe für Temperatur -->
        <div class="temperature" :style="{ backgroundColor: temperatureColor }">
          {{ temperature }}°C
        </div>
        <!-- Dynamische Farbe für Luftfeuchtigkeit -->
        <div class="humidity" :style="{ backgroundColor: humidityColor }">
          {{ humidity }}%
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
/* Anwenden des Fonts */
.room-card {
  font-family: 'Noto Sans', sans-serif;
}

/* Hauptcontainer */
.room-card {
  background-color: #f5f5f5;
  border-radius: 8px;
  padding: 1rem;
  width: 100%;
  max-width: 80%;
  height: auto;
  margin: auto;
}

/* Titel */
.room-title {
  font-size: 1.5rem;
  margin-bottom: 1rem;
  text-align: center;
}

/* Bildlayout */
.room-layout {
  position: relative;
  width: 100%;
  height: 0;
  padding-top: 56.25%; /* 16:9 Aspect Ratio */
} 

/* Raum-Bild */
.room-image {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
}

/* Temperatur- und Luftfeuchtigkeitsanzeige */
.metrics {
  position: absolute;
  right: 0;
  bottom: 0;
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

/* Dynamische Anzeige für Temperatur und Luftfeuchtigkeit */
.temperature,
.humidity {
  padding: 0.5rem;
  border-radius: 4px;
  color: white; /* Textfarbe immer weiß */
  text-align: center;
  font-weight: bold;
  min-width: 60px;
  max-width: 100px;
  font-size: calc(0.5rem + 1vw); /* Dynamische Schriftgröße */
}
</style>

<template>
  <div class="exchange-board">
    <h2>BUREAU DE CHANGE<br /><small>Exchange Office</small></h2>


    <div class="montant-container">
      <p>Montant en XPF à convertir :</p>
      <input
          type="number"
          v-model.number="montant"
          class="formMontant"
          placeholder="Montant en XPF"
      />
    </div>

    <div class="columns">
      <div class="column" v-for="(col, colIndex) in [colGauche, colDroite]" :key="colIndex">
        <TransitionGroup name="fade" tag="div">
          <div
              class="rate-row fade-enter-active glow-hover"
              :id="`rate-${index}`"
              v-for="(devise, index) in col"
              :key="devise.code"
              :style="{ animationDelay: `${index * 100}ms` }"
          >

          <div class="flag">
              <img :src="devise.urlFlag" :alt="devise.pays" />
            </div>
            <div class="name">
              <strong>{{ devise.nom }}</strong><br />
              <small>{{ devise.pays }}</small>
            </div>
            <div class="code">{{ devise.code }}</div>
            <div class="rate">
              <div class="taux">{{ data.conversion_rates[devise.code] }}</div>
              <div class="converted">{{ (data.conversion_rates[devise.code] * montant).toFixed(2) }}</div>
            </div>
          </div>
        </TransitionGroup>

      </div>
    </div>

  </div>
</template>





<script setup>
import { ref, computed, onMounted } from 'vue'

const montant = ref(1000)
const data = ref({ conversion_rates: {} })
const apiUrl = 'https://v6.exchangerate-api.com/v6/d5a20a0c605be1d85ff3ab9c/latest/XPF'

const fetchRates = async () => {
  try {
    const res = await fetch(apiUrl)
    const json = await res.json()
    if (json.result === 'success') {
      data.value = json
    } else {
      console.error('Erreur lors de la récupération des taux :', json)
    }
  } catch (error) {
    console.error('Erreur réseau :', error)
  }
}

// recall api au bout de 1h
onMounted(() => {
  fetchRates()
  setInterval(fetchRates, 3600000)
})

const devises = [
  { code: 'AUD', nom: 'Dollar australien', pays: 'Australie', urlFlag: 'https://flagcdn.com/au.svg' },
  { code: 'CAD', nom: 'Dollar canadien', pays: 'Canada', urlFlag: 'https://flagcdn.com/ca.svg' },
  { code: 'CHF', nom: 'Franc suisse', pays: 'Suisse', urlFlag: 'https://flagcdn.com/ch.svg' },
  { code: 'EUR', nom: 'Euro', pays: 'Europe', urlFlag: 'https://flagcdn.com/eu.svg' },
  { code: 'FJD', nom: 'Dollar fidjien', pays: 'Fidji', urlFlag: 'https://flagcdn.com/fj.svg' },
  { code: 'GBP', nom: 'Livre sterling', pays: 'Royaume-Uni', urlFlag: 'https://flagcdn.com/gb.svg' },
  { code: 'JPY', nom: 'Yen', pays: 'Japon', urlFlag: 'https://flagcdn.com/jp.svg' },
  { code: 'NZD', nom: 'Dollar néo-zélandais', pays: 'Nouvelle-Zélande', urlFlag: 'https://flagcdn.com/nz.svg' },
  { code: 'SGD', nom: 'Dollar de Singapour', pays: 'Singapour', urlFlag: 'https://flagcdn.com/sg.svg' },
  { code: 'THB', nom: 'Baht thaïlandais', pays: 'Thaïlande', urlFlag: 'https://flagcdn.com/th.svg' },
  { code: 'USD', nom: 'Dollar américain', pays: 'États-Unis', urlFlag: 'https://flagcdn.com/us.svg' },
  { code: 'VUV', nom: 'Vatu', pays: 'Vanuatu', urlFlag: 'https://flagcdn.com/vu.svg' },
  { code: 'XPF', nom: 'Franc Pacifique', pays: 'Nouvelle-Calédonie', urlFlag: 'https://flagcdn.com/nc.svg' }
]

const mid = Math.ceil(devises.length / 2)
const colGauche = computed(() => devises.slice(0, mid))
const colDroite = computed(() => devises.slice(mid))
</script>





<style scoped>
.exchange-board {
  max-width: 900px;
  margin: 0 auto;
  background: linear-gradient(to right, #0d47a1, #1976d2);
  color: white;
  padding: 2rem;
  border-radius: 10px;
  font-family: sans-serif;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3);
}

.formMontant{
  width: 20%;
  padding: 0.5rem;
  border: none;
  border-radius: 5px;
  font-size: 1.2rem;
  background-color: rgba(255, 255, 255, 0.1);
  color: white;
  text-align: center;
}

.exchange-board h2 {
  text-align: center;
  margin-bottom: 2rem;
  font-size: 1.8rem;
  letter-spacing: 1px;
}

.exchange-board h2 small {
  font-size: 0.8rem;
  color: #bbb;
}

.columns {
  display: flex;
  gap: 2rem;
  flex-wrap: wrap;
}

.column {
  flex: 1;
  min-width: 280px;
}

.rate-row {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background-color: rgba(255, 255, 255, 0.1);
  margin-bottom: 0.5rem;
  padding: 0.5rem 1rem;
  border-radius: 5px;
}

.flag img {
  width: 32px;
  border-radius: 4px;
}

.name {
  flex-grow: 2;
  padding-left: 1rem;
}

.code,
.rate {
  width: 80px;
  text-align: right;
  font-weight: bold;
}
.montant-container {
  text-align: center;
  margin-bottom: 2rem;
}


.rate {
  text-align: right;
}

.taux {
  font-size: 0.9rem;
  color: #ccc;
}

.converted {
  font-size: 1.1rem;
  font-weight: bold;
}

.fade-enter-active {
  animation: fadeInUp 5s ease forwards;
}
@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.glow-hover {
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.glow-hover:hover {
  transform: translateY(-3px) scale(1.01);
  box-shadow: 0 4px 15px rgba(204, 91, 232, 0.81);
  background-color: rgba(142, 84, 209, 0.62);
}

</style>


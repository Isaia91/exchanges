<template>
  <h1>Convertisseur de devises</h1>
  <p>
    Ce convertisseur de devises vous permet de convertir des montants d'une devise à une autre.
    Il utilise les taux de change fournis par l'API de <a href="https://exchangeratesapi.io/">exchangeratesapi.io</a>.
    Les taux de change sont mis à jour quotidiennement.
    Vous pouvez entrer un montant en XPF et voir combien cela vaut dans d'autres devises.
  </p>
  <input
      v-model.number="montant"
      type="number"
      class="form-control mb-4"
      placeholder="Montant en XPF"
  />

  <table class="table">
    <thead>
    <tr>
      <th>Pays</th>
      <th>Devise</th>
      <th>Taux de change</th>
      <th>Montant converti</th>

    </tr>
    </thead>
    <tbody>
      <tr v-for="devise in devises" :key="devise.code">
        <td>
          <img
              :src="devise.urlFlag"
              :alt="devise.pays"
              width="30"
              class="me-2"
          />
          {{ devise.pays }}
        </td>

        <td>{{ devise.code }}</td>
        <td>{{ data.conversion_rates[devise.code] }}</td>
        <td>{{ (data.conversion_rates[devise.code] * montant).toFixed(2) }}</td>
      </tr>
    </tbody>
  </table>
</template>

<script setup>
import jsonData from '../assets/data/data.json'
import { ref } from 'vue'

const montant = ref(1000)
const data = ref(jsonData)

const devises = [
  { code: 'AUD', pays: 'Australie', urlFlag: 'https://flagcdn.com/au.svg' },
  { code: 'CAD', pays: 'Canada', urlFlag: 'https://flagcdn.com/ca.svg' },
  { code: 'CHF', pays: 'Suisse', urlFlag: 'https://flagcdn.com/ch.svg' },
  { code: 'EUR', pays: 'Europe', urlFlag: 'https://flagcdn.com/eu.svg' },
  { code: 'FJD', pays: 'Fidji', urlFlag: 'https://flagcdn.com/fj.svg' },
  { code: 'GBP', pays: 'Royaume-Uni', urlFlag: 'https://flagcdn.com/gb.svg' },
  { code: 'JPY', pays: 'Japon', urlFlag: 'https://flagcdn.com/jp.svg' },
  { code: 'NZD', pays: 'Nouvelle-Zélande', urlFlag: 'https://flagcdn.com/nz.svg' },
  { code: 'SGD', pays: 'Singapour', urlFlag: 'https://flagcdn.com/sg.svg' },
  { code: 'THB', pays: 'Thaïlande', urlFlag: 'https://flagcdn.com/th.svg' },
  { code: 'USD', pays: 'États-Unis', urlFlag: 'https://flagcdn.com/us.svg' },
  { code: 'VUV', pays: 'Vanuatu', urlFlag: 'https://flagcdn.com/vu.svg' },
  { code: 'XPF', pays: 'Nouvelle-Calédonie', urlFlag: "https://flagcdn.com/nc.svg" }
]
</script>


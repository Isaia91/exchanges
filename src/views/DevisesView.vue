<template>
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
    <tr>
      <td>Australie</td>
      <td>AUD</td>
      <td>{{ data.conversion_rates.AUD }}</td>
      <td>{{ (data.conversion_rates.AUD * montant).toFixed(2) }}</td>
    </tr>
    <tr>
      <td>Canada</td>
      <td>CAD</td>
      <td>{{ data.conversion_rates.CAD }}</td>
      <td>{{ (data.conversion_rates.CAD * montant).toFixed(2) }}</td>
    </tr>
    <tr>
      <td>Suisse</td>
      <td>CHF</td>
      <td>{{ data.conversion_rates.CHF }}</td>
      <td>{{ (data.conversion_rates.CHF * montant).toFixed(2) }}</td>
    </tr>
    <tr>
      <td>Europe</td>
      <td>EUR</td>
      <td>{{ data.conversion_rates.EUR }}</td>
      <td>{{ (data.conversion_rates.EUR * montant).toFixed(2) }}</td>
    </tr>
    <tr>
      <td>Fidji</td>
      <td>FJD</td>
      <td>{{ data.conversion_rates.FJD }}</td>
      <td>{{ (data.conversion_rates.FJD * montant).toFixed(2) }}</td>
    </tr>
    <tr>
      <td>Royaume-Uni</td>
      <td>GBP</td>
      <td>{{ data.conversion_rates.GBP }}</td>
      <td>{{ (data.conversion_rates.GBP * montant).toFixed(2) }}</td>
    </tr>
    <tr>
      <td>Japon</td>
      <td>JPY</td>
      <td>{{ data.conversion_rates.JPY }}</td>
      <td>{{ (data.conversion_rates.JPY * montant).toFixed(2) }}</td>
    </tr>
    <tr>
      <td>New-Zeland</td>
      <td>NZD</td>
      <td>{{ data.conversion_rates.NZD }}</td>
      <td>{{ (data.conversion_rates.NZD * montant).toFixed(2) }}</td>
    </tr>
    <tr>
      <td>Singapour</td>
      <td>SGD</td>
      <td>{{ data.conversion_rates.SGD }}</td>
      <td>{{ (data.conversion_rates.SGD * montant).toFixed(2) }}</td>
    </tr>
    <tr>
      <td>Thailand</td>
      <td>THB</td>
      <td>{{ data.conversion_rates.THB }}</td>
      <td>{{ (data.conversion_rates.THB * montant).toFixed(2) }}</td>
    </tr>
    <tr>
      <td>Etat-Unis</td>
      <td>USD</td>
      <td>{{ data.conversion_rates.USD }}</td>
      <td>{{ (data.conversion_rates.USD * montant).toFixed(2) }}</td>
    </tr>
    <tr>
      <td>Vanuatu</td>
      <td>VUV</td>
      <td>{{ data.conversion_rates.VUV }}</td>
      <td>{{ (data.conversion_rates.VUV * montant).toFixed(2) }}</td>
    </tr>
    <tr>
      <td>Nouvelle-Calédonie</td>
      <td>XPF</td>
      <td>{{ data.conversion_rates.XPF }}</td>
      <td>{{ (data.conversion_rates.XPF * montant).toFixed(2) }}</td>
    </tr>
    </tbody>
  </table>
</template>

<script>
import jsonData from '../assets/data/data.json'
import { ref } from 'vue'

export default {
  name: 'DevisesView',
  setup() {
    const data = ref(jsonData)
    const montant = ref(1000)

    return { data, montant }
  }
}
</script>

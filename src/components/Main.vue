<template>
  <v-container>
    <v-layout text-xs-center wrap>
      <v-flex xs10 class="pr-2">
        <v-text-field solo v-model="amount" label="Amount" single-line class="custom cheight" />
      </v-flex>
      <v-flex xs2>
        <v-btn color="primary" @click="submit" depressed block large>Submit</v-btn>
      </v-flex>
    </v-layout>

    <v-data-table :headers="headers" :items="result" class="elevation-1" :rows-per-page-items="[10,25,{'text':'All','value':-1}]">
      <template slot="items" slot-scope="props">
        <td>Rp {{ props.item.notes }}</td>
        <td>x{{ props.item.counter }}</td>
      </template>
    </v-data-table>
  </v-container>
</template>
<style scoped>
  .custom{
    margin-top: 5px;
  }
  .cheight >>> .v-text-field.v-text-field--solo.v-input__control {
    max-height: 45px !important;
  }
</style>
<script>
import Money from '../lib/money.js'
  export default {
    data: () => ({
      amount : null,
      result : []
    }),

    computed : {
      headers(){
        return [
          { text:'Value', value:'notes', sortable: false},
          { text:'Counter', value:'counter', sortable: false}
        ];
      }
    },

    methods : {
      submit(){
        const amount = this.filterString(this.amount)
        const money = Money.denomination(amount);
        this.result = money;
      },

      filterString(val){
        const result = val.replace(new RegExp(/([A-Z]|[a-z]|[.]|[^,\w])/g), '').trim();
        console.log(result);
        return parseInt(result);
      }
    },

    created(){},

    watch : {}
  }
</script>

<style>

</style>

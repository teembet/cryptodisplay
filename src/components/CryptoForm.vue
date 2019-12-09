<template>
  <div id="crypto-form">
   <div class="tablediv" style="overflow-x:auto;">
     
      <table>
    <thead>
      <tr>
        <th v-for="column in columns" :key="column.name">{{column.label}}</th>
        
      </tr>
    </thead>
    <tbody>
<tr v-for="crypto in paginatedData" :key="crypto.id" class="datarow">
    <td>{{crypto.name}}                 
  </td>
  <td>
   {{crypto.symbol}}                  
  </td>
  <td>{{crypto.price_usd}}                  
  </td>
  <td>{{crypto.tsupply}} {{crypto.symbol}}                       
  </td>
</tr>
    </tbody>
 </table>

   </div>
   <div class="btndiv">
     <tr id="btntr">
       <td>
 
<button id="btn1" @click="prevPage" :hidden="pageNumber==0"> &larr; Prev  </button>
 <button id="btn2" @click="nextPage"  :hidden="pageNumber >= pageCount -1">Next &#8594;</button></td>
</tr>
</div>

  </div>
</template>

<script>
export default {
  name: 'crypto-form',
data(){
  let columns=[
    {label:'💰 Coin', name: 'name'},
{label:'📄 Code', symbol:'symbol'},
{label:'🤑 Price', price_usd:'price_usd'},
 {label:'📉 Total Supply', tsupply:'tsupply'}
          
  ];

 
  return{
    pageNumber:0,
    columns:columns
  }
},
  

 props: {
        cryptos: {
          type:Array,
        required:true
        },
        size:{
          type:Number,
          required:false,
          default:10
        },

 },

 methods: {
   nextPage(){
     this.pageNumber++;
   },
   prevPage(){
     this.pageNumber--;
   }
 },
computed:{
  pageCount(){
    let l=this.cryptos.length,
    s=this.size;
    return Math.ceil(l/s);
  },
paginatedData(){
  const start=this.pageNumber * this.size,
  end= start + this.size;
  return this.cryptos.slice(start,end);
}

}


}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.datarow:nth-child(odd){
  background-color: #f2f2f2;
}

.tablediv{
display: flex;
justify-content: center;
align-items: center;
width: auto;



}

#btn1{
  border: none;
   padding: 2px;
  background: none;
  font-weight: bold;
  

}

#btn2{
  border: none;
  padding: 2px;
  background: none;
  font-weight: bold;

}

th{
  padding: 10px;
  text-align: left
}
td{
  padding: 10px;
  text-align: left
}
table{
  border: 20px;
  border-color: black;
  border-collapse: collapse;
  width: 100%;
}
.btndiv{
  background-color: #f2f2f2;
overflow: hidden;
}

#btntr{
  float: right;
 margin-left: -50%

}
</style>

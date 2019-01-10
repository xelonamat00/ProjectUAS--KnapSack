<template>
  <v-container>
    <!-- List Image -->
    <h2>Daftar Produk</h2> <br>
      <v-layout row wrap>
        <ul class="products" v-for="(item, index) in itemsWeight" :key="index">
            <li>
                <img :src= item.url width="50%">
                <div></div>
                <h4>{{ item.nama }}</h4>
                <p>{{ item.berat }} Kg <br> Rp{{ item.harga }} <br> (density: {{item.density}})</p>
                <p></p>
            </li>
        </ul>
      </v-layout>

      <v-layout>
        <v-flex md2 xs2 offset-sm3>
          <img src="@/assets/kurir_motor.png" width="300px">
        </v-flex>
      </v-layout>
    
      <form @submit.prevent="excute()">
        <v-layout row wrap>
          <v-flex md3 xs2 offset-sm3>
            <v-text-field
              label="Kapasitas Maksimal (kg)"
              v-model="maxCapacity"
            ></v-text-field>
          </v-flex>
            <v-btn type="submit" round color="primary" dark>Kalkulasi</v-btn>
        </v-layout>
      </form> 

      <!-- <v-layout row wrap>
        <ul class="products" v-for="(item, index) in resultByWeight" :key="index">
            <li>
                <img :src= item.url width="50%">
                <div></div>
                <h4>{{ item.nama }}</h4>
                <p>{{ item.berat }} Kg <br> Rp{{ item.harga }}</p>
                <p></p>
            </li>
        </ul>
      </v-layout> -->
      <!-- {{resultByWeight.nama}} -->

    <!-- <v-layout>
      <table class="table mt-3">
        <thead>
            <tr>
                <th>Berat</th>
                <th>Profit</th>
                <th>Density</th>
                <th>Status</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="(init, index) in items" :key="index">
                <td>{{init.berat}}</td>
                <td>{{init.harga}}</td>
                <td>{{init.density}}</td>
                <td>{{init.status}}</td>
            </tr>
        </tbody>
    </table>
    </v-layout>

  

    <v-layout>
      <v-tabs fixed-tabs>
        <v-tab
          v-for="n in 3"
          :key="n"
        >
          Item {{ n }}
        </v-tab>
      </v-tabs>
    </v-layout> -->

    <v-layout row wrap v-if="display">
      <v-flex>
        <v-layout>
          <h2>By Weight</h2>
        </v-layout>
        <v-layout row wrap>
            <ul class="products" v-for="(item, index) in resultByWeight" :key="index">
                <li>
                    <img :src= item.url width="50%">
                    <div></div>
                    <h4>{{ item.nama }}</h4>
                    <p>{{ item.berat }} Kg <br> Rp{{ item.harga }}<br> (density: {{item.density}})</p>
                    <p></p>
                </li>
            </ul>
          </v-layout>
          <v-layout>
            <div>
              <span class="indigo--text lighten-1"><h3>Total Berat: {{totalBerat}} Kg</h3>
              <h3>Total Profit: Rp{{totalProfitt}} </h3>
              <h3>Total Densitas: {{total_densityWeight}}</h3></span>
            </div>
          </v-layout>
      </v-flex>
      
      <!-- By Profit -->
        <v-flex mt-4>
          <v-layout>
            <h2>By Profit</h2>
          </v-layout>
          <v-layout row wrap>
            <ul class="products" v-for="(item, index) in resultByProfit" :key="index">
                <li>
                    <img :src= item.url width="50%">
                    <div></div>
                    <h4>{{ item.nama }}</h4>
                    <p>{{ item.berat }} Kg <br> Rp{{ item.harga }}<br> (density: {{item.density}})</p>
                    <p></p>
                </li>
            </ul>
          </v-layout>
          <v-layout>
            <div>
              <span class="indigo--text lighten-1"><h3>Total Berat: {{totalBeratProfit}} Kg</h3>
              <h3>Total Profit: Rp{{totalProfittProfit}} </h3>
              <h3>Total Densitas: {{total_densityProfit}}</h3></span>
            </div>
          </v-layout>
        </v-flex>
      

      <!-- By Density -->
        <v-flex mt-4>
          <v-layout>
            <h2>By Density</h2>
          </v-layout>
          <v-layout row wrap>
            <ul class="products" v-for="(item, index) in resultByDensity" :key="index">
                <li>
                    <img :src= item.url width="50%">
                    <div></div>
                    <h4>{{ item.nama }}</h4>
                    <p>{{ item.berat }} Kg <br> Rp{{ item.harga }}<br> (density: {{item.density}})</p>
                    <p></p>
                </li>
            </ul>
          </v-layout>
          <v-layout>
            <div>
              <span class="indigo--text lighten-1"><h3>Total Berat: {{totalBeratDensity}} Kg</h3>
              <h3>Total Profit: Rp{{totalProfittDensity}} </h3>
              <h3>Total Densitas: {{total_densityDensity}}</h3></span>
            </div>
          </v-layout>
        </v-flex>
      
    </v-layout>

    <!-- <br><br>
    <v-layout justify-center>
      <v-flex>
        <v-tabs>
          <v-tab>Berdasarkan Berat</v-tab>
          <v-tab>Berdasarkan Profit</v-tab>
          <v-tab>Berdasarkan Densitas</v-tab>

        <v-tab-item>
          <v-layout row wrap>
            <ul class="products" v-for="(item, index) in resultByWeight" :key="index">
                <li>
                    <img :src= item.url width="50%">
                    <div></div>
                    <h4>{{ item.nama }}</h4>
                    <p>{{ item.berat }} Kg <br> Rp{{ item.harga }}</p>
                    <p></p>
                </li>
            </ul>
            <div>
              <p>Total Berat: {{totalBerat}}</p><br>
              <p>Total Profit: {{totalProfitt}}</p>
            </div>
          </v-layout>
        </v-tab-item>

        <v-tab-item>
          <v-layout row wrap>
            <ul class="products" v-for="(item, index) in resultByProfit" :key="index">
                <li>
                    <img :src= item.url width="50%">
                    <div></div>
                    <h4>{{ item.nama }}</h4>
                    <p>{{ item.berat }} Kg <br> Rp{{ item.harga }}</p>
                    <p></p>
                </li>
            </ul>
            <div>
              <p>Total Berat: {{totalBeratProfit}}</p><br>
              <p>Total Profit: {{totalProfittProfit}}</p>
            </div>
          </v-layout>
        </v-tab-item>

        <v-tab-item>
          <v-layout row wrap>
            <ul class="products" v-for="(item, index) in resultByDensity" :key="index">
                <li>
                    <img :src= item.url width="50%">
                    <div></div>
                    <h4>{{ item.nama }}</h4>
                    <p>{{ item.berat }} Kg <br> Rp{{ item.harga }}</p>
                    <p></p>
                </li>
            </ul>
            <div>
              <p>Total Berat: {{totalBeratDensity}}</p><br>
              <p>Total Profit: {{totalProfittDensity}}</p>
            </div>
          </v-layout>
        </v-tab-item>


        </v-tabs>
      </v-flex>
    </v-layout> -->
  </v-container>
</template>

<script>
  export default {
    
    // computed: {
    //   totalBerat() {
    //     return this.resultByWeight
    //   }
    // },
    methods: {
      totalWeight() {
        this.resultByWeight.forEach(entry=> {
          this.totalBerat += entry.berat
          this.totalProfitt += entry.harga
          this.total_densityWeight += entry.density
          
        })
      },
      totalDensity() {
        this.resultByDensity.forEach(entry=> {
          this.totalBeratDensity += entry.berat
          this.totalProfittDensity += entry.harga
          this.total_densityDensity += entry.density
        })
      },
      totalProfit() {
        this.resultByProfit.forEach(entry=> {
          this.totalBeratProfit += entry.berat
          this.totalProfittProfit += entry.harga
          this.total_densityProfit += entry.density
        })
      },
      sortAscendent () {
          function compare (a, b) {
              if (a.berat < b.berat) {
                  return -1
              }
              if (a.berat > b.berat) {
                  return 1
              }
              return 0
          }
          this.isSortedWeight = true
          // this.initsAsc = JSON.parse(JSON.stringify(this.inits))
          this.tempItemsWeight = Array.from(this.itemsWeight)
      //    console.log(this.initsAsc)
          return this.tempItemsWeight.sort(compare)
      },
      sortDescendent () {
        function compare (a, b) {
              if (a.harga < b.harga) {
                  return 1
              }
              if (a.harga > b.harga) {
                  return -1
              }
              return 0
          }
          this.isSortedProfit = true
          this.tempItemsProfit = Array.from(this.itemsProfit)
          return this.tempItemsProfit.sort(compare)
      },
      sortDescendentDencity() {
        function compare(a, b){
          if(a.density < b.density){
            return 1
          }
          if(a.density > b.density){
            return -1
          }
          return 0
        }
        this.isSortedDensity = true,
        this.tempItemsDensity = Array.from(this.itemsDensity)
        return this.tempItemsDensity.sort(compare)
      },
      greedyByDesntiy(){
        this.sortDescendentDencity()
        var i = 0
        while(i < this.itemsDensity.length){
          if(this.totalBobotDensity + this.tempItemsDensity[i].berat <= this.maxCapacity){
            for(var a = 0; a < this.itemsDensity.length; a++){
              if(JSON.stringify(this.tempItemsDensity[i]) === JSON.stringify(this.itemsDensity[a])){
                this.itemsDensity[a].status = 1
                this.totalProfitDensity += this.itemsDensity[a].profit
                this.totalBobotDensity += parseInt(this.tempItemsDensity[i].berat)
                console.log(this.totalBobotDensity)
                break
              }
            }
          }
          i++
        }
        this.resultByDensity = this.itemsDensity.filter(function(item){return item.status > 0})
        // console.log(this.resultByDensity)
        this.totalDensity()
      },
      greedyByWeight () {
        this.sortAscendent()
        var i = 0
        while(i < this.itemsWeight.length){
            if(this.totalBobotWeight + this.tempItemsWeight[i].berat<= this.maxCapacity){
                for(var a = 0; a < this.itemsWeight.length; a++){
                  if(JSON.stringify(this.tempItemsWeight[i]) === JSON.stringify(this.itemsWeight[a])){
                    this.itemsWeight[a].status = 1
                    this.totalProfitWeight += this.itemsWeight[a].profit
                    this.totalBobotWeight += parseInt(this.tempItemsWeight[i].berat)
                    console.log(this.totalBobotWeight)
                    break
                }
              }
            }
          i++
        }
        this.resultByWeight = this.itemsWeight.filter(function(item){return item.status > 0})
        // console.log(this.resultByWeight)
        this.totalWeight()
      },
      greedyByProfit () {
        this.sortDescendent()
        var i = 0
        while(i < this.itemsProfit.length){
            if(this.totalBobotProfit + this.tempItemsProfit[i].berat <= this.maxCapacity){
                for(var a = 0; a < this.itemsProfit.length; a++){
                  if(JSON.stringify(this.tempItemsProfit[i]) === JSON.stringify(this.itemsProfit[a])){
                    this.itemsProfit[a].status = 1
                    this.totalProfitProfit += this.itemsProfit[a].profit
                    this.totalBobotProfit += parseInt(this.tempItemsProfit[i].berat)
                    console.log(this.totalBobotProfit)
                    break
                }
              }
            }
          i++
        }
        this.resultByProfit = this.itemsProfit.filter(function(item){return item.status > 0})
        this.totalProfit()
      },
      excute() {
        this.greedyByDesntiy()
        this.greedyByWeight()
        this.greedyByProfit()
        this.display = true
      }
    },


  data() {
      return {
        display: false,


        // byWeight
        totalBerat: 0,
        totalProfitt: 0,
        total_densityWeight:0,
        densityWeight: null,
        totalBobotWeight: 0,
        totalProfitWeight: 0,
        maxCapacity: null,
        tempItemsWeight: [],
        isSortedWeight: false,
        resultByWeight: [],
        itemsWeight: [
          {url: require('@/assets/dus_kecap_bango.jpg'), nama: 'Kecap Bango', berat: 5, harga: 99000, density: 19800, status: 0},
          {url: require('@/assets/dus_kopi.jpg'), nama: 'Kopi Kapal Api', berat: 3, harga: 109000, density: 36333, status: 0},
          {url: require('@/assets/dus_kratindeng.jpg'), nama: 'Kratindeng', berat: 6, harga: 130000, density: 21666, status: 0},
          {url: require('@/assets/dus_pocari_sweat.jpg'), nama: 'Pocari Sweat', berat: 8, harga: 125000, density: 15625, status: 0},
          {url: require('@/assets/beras_fortune.jpg'), nama: 'Beras Fortune', berat: 30, harga: 145000, density: 4834, status: 0},
          {url: require('@/assets/gula_gmp.jpg'), nama: 'Gula Pasir GMP', berat: 50, harga: 250000, density: 5000, status: 0},
          {url: require('@/assets/dus_indomie.jpg'), nama: 'Indomie Goreng', berat: 5, harga: 79000, density: 15800, status: 0},
          {url: require('@/assets/dus_indomie_rendang.jpg'), nama: 'Goreng Rendang', berat: 5, harga: 85000, density: 17000, status: 0},
          {url: require('@/assets/dus_sirup_marjan.jpg'), nama: 'Sirup Marjan', berat: 7, harga: 119000, density: 17000, status: 0},
          {url: require('@/assets/dus_teh_kotak.jpg'), nama: 'Teh Kotak', berat: 6, harga: 60000, density: 10000, status: 0},
          {url: require('@/assets/beras_rojolele.jpg'), nama: 'Beras Rojo Lele', berat: 50, harga: 350000, density: 5000, status: 0},
          {url: require('@/assets/dus_sunlight.jpg'), nama: 'Sunlight', berat: 5, harga: 70000, density: 14000, status: 0},
          {url: require('@/assets/karung_segitiga_biru.jpg'), nama: 'Tepung Segitiga Biru', berat: 50, harga: 215000, density: 4300, status: 0},
          {url: require('@/assets/minyak_nabati.jpg'), nama: 'Minyak Nabati', berat: 15, harga: 60000, density: 4000, status: 0},
        ],

        // by Profit

        totalBeratProfit: 0,
        totalProfittProfit: 0,
        total_densityProfit:0,
        densityProfit: null,
        totalBobotProfit: 0,
        totalProfitProfit: 0,
        maxCapacity: null,
        tempItemsProfit: [],
        isSortedProfit: false,
        resultByProfit: [],
        itemsProfit: [
          {url: require('@/assets/dus_kecap_bango.jpg'), nama: 'Kecap Bango', berat: 5, harga: 99000, density: 19800, status: 0},
          {url: require('@/assets/dus_kopi.jpg'), nama: 'Kopi Kapal Api', berat: 3, harga: 109000, density: 36333, status: 0},
          {url: require('@/assets/dus_kratindeng.jpg'), nama: 'Kratindeng', berat: 6, harga: 130000, density: 21666, status: 0},
          {url: require('@/assets/dus_pocari_sweat.jpg'), nama: 'Pocari Sweat', berat: 8, harga: 125000, density: 15625, status: 0},
          {url: require('@/assets/beras_fortune.jpg'), nama: 'Beras Fortune', berat: 30, harga: 145000, density: 4834, status: 0},
          {url: require('@/assets/gula_gmp.jpg'), nama: 'Gula Pasir GMP', berat: 50, harga: 250000, density: 5000, status: 0},
          {url: require('@/assets/dus_indomie.jpg'), nama: 'Indomie Goreng', berat: 5, harga: 79000, density: 15800, status: 0},
          {url: require('@/assets/dus_indomie_rendang.jpg'), nama: 'Goreng Rendang', berat: 5, harga: 85000, density: 17000, status: 0},
          {url: require('@/assets/dus_sirup_marjan.jpg'), nama: 'Sirup Marjan', berat: 7, harga: 119000, density: 17000, status: 0},
          {url: require('@/assets/dus_teh_kotak.jpg'), nama: 'Teh Kotak', berat: 6, harga: 60000, density: 10000, status: 0},
          {url: require('@/assets/beras_rojolele.jpg'), nama: 'Beras Rojo Lele', berat: 50, harga: 350000, density: 5000, status: 0},
          {url: require('@/assets/dus_sunlight.jpg'), nama: 'Sunlight', berat: 5, harga: 70000, density: 14000, status: 0},
          {url: require('@/assets/karung_segitiga_biru.jpg'), nama: 'Tepung Segitiga Biru', berat: 50, harga: 215000, density: 4300, status: 0},
          {url: require('@/assets/minyak_nabati.jpg'), nama: 'Minyak Nabati', berat: 15, harga: 60000, density: 4000, status: 0},
        ],











        // by Density
        totalBeratDensity: 0,
        totalProfittDensity: 0,
        total_densityDensity: 0,
        densityDensity: null,
        totalBobotDensity: 0,
        totalProfitDensity: 0,
        maxCapacityDensity: null,
        tempItemsDensity: [],
        isSortedDensity: false,
        resultByDensity: [],
        itemsDensity: [
          {url: require('@/assets/dus_kecap_bango.jpg'), nama: 'Kecap Bango', berat: 5, harga: 99000, density: 19800, status: 0},
          {url: require('@/assets/dus_kopi.jpg'), nama: 'Kopi Kapal Api', berat: 3, harga: 109000, density: 36333, status: 0},
          {url: require('@/assets/dus_kratindeng.jpg'), nama: 'Kratindeng', berat: 6, harga: 130000, density: 21666, status: 0},
          {url: require('@/assets/dus_pocari_sweat.jpg'), nama: 'Pocari Sweat', berat: 8, harga: 125000, density: 15625, status: 0},
          {url: require('@/assets/beras_fortune.jpg'), nama: 'Beras Fortune', berat: 30, harga: 145000, density: 4834, status: 0},
          {url: require('@/assets/gula_gmp.jpg'), nama: 'Gula Pasir GMP', berat: 50, harga: 250000, density: 5000, status: 0},
          {url: require('@/assets/dus_indomie.jpg'), nama: 'Indomie Goreng', berat: 5, harga: 79000, density: 15800, status: 0},
          {url: require('@/assets/dus_indomie_rendang.jpg'), nama: 'Goreng Rendang', berat: 5, harga: 85000, density: 17000, status: 0},
          {url: require('@/assets/dus_sirup_marjan.jpg'), nama: 'Sirup Marjan', berat: 7, harga: 119000, density: 17000, status: 0},
          {url: require('@/assets/dus_teh_kotak.jpg'), nama: 'Teh Kotak', berat: 6, harga: 60000, density: 10000, status: 0},
          {url: require('@/assets/beras_rojolele.jpg'), nama: 'Beras Rojo Lele', berat: 50, harga: 350000, density: 5000, status: 0},
          {url: require('@/assets/dus_sunlight.jpg'), nama: 'Sunlight', berat: 5, harga: 70000, density: 14000, status: 0},
          {url: require('@/assets/karung_segitiga_biru.jpg'), nama: 'Tepung Segitiga Biru', berat: 50, harga: 215000, density: 4300, status: 0},
          {url: require('@/assets/minyak_nabati.jpg'), nama: 'Minyak Nabati', berat: 15, harga: 60000, density: 4000, status: 0},
        ],
      }
    }




  }
</script>




































<style>
ul.products li {
    width: 150px;
    display: inline-block;
    vertical-align: top;
}

ul, ol{
  padding-left: 0px;
}

.border{
  border-radius: 25px;
  border: 2px solid #73AD21;
  padding : 20px;
  width: 200px;
  height: 150px;
}




</style>

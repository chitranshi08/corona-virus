<template>
    <div>
        <h1>COVID- 19 TRACKER</h1>
        <div class="mainContainer">
            <img src="./../assets/virus.jpg" alt="">
            <div class="detailPage">
                <div>Today's New Confirmed Cases: {{NewConfirmedDetail}}</div>
                <div>Today's Total Confirmed Cases: {{TotalConfirmedDetail}}</div>
                <div>New Death Cases: <span class="death">{{NewDeathDetail}}</span></div>
                <div>Total Death Cases: <span class="death">{{TotalDeathDetail}}</span></div>
                <div>New Recovered Cases: <span class="recovered">{{NewRecoveredDetail}}</span></div>
                <div>Total Recovered Cases: <span class="recovered">{{TotalRecoveredDetail}}</span></div>
                <div class="countryList">Country List</div>
                <select name="" id="" v-model="selectedCountry" @change="showDetail">
            <option :value="Country" v-for="Country in Countries">{{Country.Country}}</option>
        </select>
            </div>
        </div>
        <div v-show="showLoader" class="loader">
          <img class="imageLoader" src="./../assets/loader.gif" alt="">
        </div>
    </div>
</template>
<script>
export default {
    name: 'CovidDetail',
    data: () => ({
        NewConfirmedDetail: null,
        TotalConfirmedDetail: null,
        NewDeathDetail: null,
        TotalDeathDetail: null,
        NewRecoveredDetail: null,
        TotalRecoveredDetail: null,
        Countries: null,
        selectedCountry:null,
        showLoader:false,

    }),

    created() {
      this.showLoader = true
        fetch("https://api.covid19api.com/summary")
            .then((response) => { return response.json() })
            .then((response) => {
                console.log(response)
                this.NewConfirmedDetail = response.Global.NewConfirmed
                this.TotalConfirmedDetail = response.Global.TotalConfirmed
                this.NewDeathDetail = response.Global.NewDeaths
                this.TotalDeathDetail = response.Global.TotalDeaths
                this.NewRecoveredDetail = response.Global.NewRecovered
                this.TotalRecoveredDetail = response.Global.TotalRecovered
                this.Countries = response.Countries



            })
            .finally(()=>{
                  this.showLoader = false
                })

    },
    methods:{
      showDetail(){
        this.showLoader = true
        this.NewConfirmedDetail = this.selectedCountry.NewConfirmed
        this.TotalConfirmedDetail = this.selectedCountry.TotalConfirmed
        this.NewDeathDetail = this.selectedCountry.NewDeaths
        this.TotalDeathDetail = this.selectedCountry.TotalDeaths
        this.NewRecoveredDetail = this.selectedCountry.NewRecovered
        this.TotalRecoveredDetail = this.selectedCountry.TotalRecovered
        this.showLoader = false
      }

    }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
    margin: 40px 0 0;
}

ul {
    list-style-type: none;
    padding: 0;
}

li {
    display: inline-block;
    margin: 0 10px;
}

a {
    color: #42b983;
}

img {
    height: 400px;
    width: 400px;
}

.mainContainer {
    display: flex;
    justify-content: space-around;
}

.detailPage {
    color: white;
    font-weight: bold;
    font-size: 25px;
    text-align:left;

}

.detailPage>div {
    margin-bottom: 20px;

}

.death {
    color: red;
}

.recovered {
    color: green;
}

h1 {
    margin-bottom: 50px;
    font-weight: bold;
}
.countryList{
  margin-bottom:0 !important;
  font-size: 20px;
}
.loader{
  height: 100vh;
  width:100vw;
  position: fixed;
  top:0;
  left:0;
  background-color: rgba(255,255,255,0.6);
  display: flex;
  justify-content: center;
  align-items: center;

}
.imageLoader{
  height:30px;
  width:30px;
}
</style>
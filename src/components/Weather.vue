<script >
export default {
  data() {
    return {
      cityName: " ",
      response: "",
      responseResult: "",
    };
  },
  methods: {
    getCityName() {
      console.log(this.cityName);

      console.log(this.cityName);
    },
    getWeather(data) {
      console.log(data);
    },
    async setResponse() {
      this.response = await fetch(
        `https://api.openweathermap.org/data/2.5/forecast?q=${this.cityName}&units=metric&appid=0fd46823f4ba7ed3290b352a7ad1d0d1`,
        {
          method: "GET",
        }
      );
      //  console.log("response "+ this.response)
      return this.response;
    },
    async setResponseResult() {
      this.responseResult = await this.response.json();
      //  console.log("response result "+ this.responseResult)
      return this.responseResult;
    },
    getData() {
      this.setResponse();
      this.setResponseResult();
      this.getWeather(this.responseResult.list);
    },
  },
};
</script>

<template>
  <div>
    <div class="container">
      <div class="content-wrp">
        <h1>Weather app</h1>
      <div class="field-wrp">
        <input
        class="input"
        type="text"
        placeholder="Enter city"
        v-model="cityName"
      />

      <button class="submit-btn" @click="getData()">submit</button>
      </div>
 
      <h2>{{ cityName }}</h2>
      <div class="list-wrap">
        <div class="list" v-for="item in responseResult.list" :key="item">
          <h3 class="date">
            {{ item.dt_txt }}
          </h3>
          <p class="temp">{{ item.main.temp }}°C</p>
          <p class="weather">{{ item.weather[0].description }}</p>
        </div>
      </div>
      </div>
     
    </div>
  </div>
</template>
<style>
.content-wrp{
  display: flex;
  flex-direction: column;
  padding: 200px 0 200px 0;
}
.field-wrp{
  margin-top: 30px;
  width: 100%;
  display: flex;
  justify-content: space-between;
  column-gap: 10px
}
h1{
  margin: 0 auto;
}
input{
  display: block;
  width: 100%;
  background-color:#aaa1ff ;
  border: none;
  border-radius: 15px;
  color: #fff;
  padding: 0 20px;
}
input:focus{
  outline: none;
}
.submit-btn{
  display: block;
  width: 200px;
  height: 50px;
  background-color: #5c5e92;
  border: none;
  border-radius: 15px;
  color: #fff;
  text-transform: capitalize;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s;
}
.submit-btn:hover{
  background-color:#aaa1ff ;
}
.list-wrap {
  display: flex;
  overflow: auto;
}
.list {
  min-width: 150px;
  display: block;
  padding: 10px;
  border: 1px #ffffff34 solid;
  border-radius: 10px;
  margin-right: 20px;
}
</style>
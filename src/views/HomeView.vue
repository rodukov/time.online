<template>
  <div class="home">

    {{ request_data }}
    <!--div class="repository" v-for="item in request_data" :key="item">
      {{ item }}
    </div-->
				<!-- Timer -->
				<div class="main timer" id="maintimer">
					<!--h1 style="letter-spacing: 0px; font-weight: 400;">Collection starts at:</!--h1-->
					<div class="countdown">
						<h1 class="wstart" id="westartsat">Whitelist starts at:</h1>
					  <div>
						<span class="number months"></span>
						<span class="date_name">Months</span>
					  </div>
					   <div>
						<span class="number days"></span>
						<span class="date_name">Days</span>
					  </div>
					   <div>
						<span class="number hours"></span>
						<span class="date_name">Hours</span>
					  </div>
					   <div>
						<span class="number minutes"></span>
						<span class="date_name">Minutes</span>
					  </div>
					   <div>
						<span class="number seconds"></span>
						<span class="date_name">Seconds</span>
					  </div>
					</div>
				  </div>

  </div>
</template>


<script>
import axios from 'axios'


export default {
  name: 'Home',
  data() { 
    return {
      request_data: []
    }
  },
  mounted() {
    this.time()
    let timestampPlus;
let plus = 3;
    let time = this.request_data;
    console.log(time)
    let z = JSON.parse(time).utc_datetime;
    let time1 = new Date(z).getTime();
    timestampPlus = time1 + (plus * 60 * 60 * 1000);
    let timePlus = new Date(timestampPlus);
    let result = timePlus.toUTCString();  
    date = time1
    console.log(result); 
    console.log({z, time1, timestampPlus, timePlus, result})


// timestampPlus
// const newDate = newXM Date('sep 12 22 23:59:59').getTime()
const newDate = moment.utc("2022-11-17 18:00:00").unix()*1000
const countdown = setInterval(() => {

// let date;


let diff = newDate - timestampPlus
timestampPlus = timestampPlus + 1000


let month =  Math.floor((diff % (1000 * 60 * 60 * 24 * (365.25 / 12) * 365)) / (1000 * 60 * 60 * 24 * (365.25 / 12)))
let days = Math.floor(diff % (1000 * 60 * 60 * 24 * (365.25 / 12)) / (1000 * 60 * 60 * 24))
let hours =  Math.floor(diff % (1000 * 60 * 60 * 24) / (1000 * 60 * 60))
let minutes = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60))
let seconds = Math.floor((diff % (1000 * 60)) / 1000)

    document.querySelector(".seconds").innerHTML = seconds < 10 ? '0' + seconds : seconds
    document.querySelector(".minutes").innerHTML = minutes < 10 ? '0' + minutes :minutes
    document.querySelector(".hours").innerHTML = hours < 10 ? '0' + hours : hours
    document.querySelector(".days").innerHTML = days < 10 ? '0' + days : days
    document.querySelector(".months").innerHTML = month < 10 ? '0' + month : month

if(diff === 0){
clearInterval(countdown)
        document.querySelector(".countdown").innerHTML = 'Check our social media'
}

}, 1000)

  },
  methods: {
    async time() {
      await axios
        .get('https://worldtimeapi.org/api/timezone/Europe/London')
        .then(response => (this.request_data = response["data"]))

        // .catch(function (error) { this.error_axios = error.status })
    }
  }
}
</script>
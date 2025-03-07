<template>
  <v-container>
    <v-row>
      <v-col cols="12" sm="6">
        <h1 class="text-h3 mb-8 mt-2 text-uppercase">{{ msg }}</h1>

        <v-sheet class="rounded" width="300">
          <v-form fast-fail @submit.prevent>
            <v-text-field v-model="age" :rules="ageNumberRules" label="Enter Your Age"></v-text-field>

            <v-text-field v-model="weight" :rules="weightKgRules" label="Enter Your Weight"></v-text-field>

            <v-text-field v-model="height" :rules="heightCmRules" label="Enter Your Height"></v-text-field>


            <v-btn class="mt-2" type="submit" block @click="getValue" color="success">Submit</v-btn>
          </v-form>
        </v-sheet>
        <p class="mt-6 pa-1 text-h6" v-if="result" >BMI: {{ result }} ({{ bmiCategory }})</p>
       
      </v-col>

      <v-col cols="12" sm="6">
        <h2 class="text-h4 text-uppercase font-weight-bold mt-5">Who adult bmi categories</h2>

        <v-table class="mt-6 mb-4 rounded">
          <thead>
            <tr class="text-h5 text-uppercase bg-black">
                <th>BMI</th>
                <th>Category</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="item in bmiTable" :key="item.name" :class="getHoverCategory(item.categories)" class="text-h6">
              <td>{{ item.name }}</td>
              <td>{{ item.categories }}</td>

            </tr>
          </tbody>
        </v-table>
      </v-col>
    </v-row>

    
  </v-container>

</template>
  
  <script>
  export default {
    name: 'BmiCalculator',
   
    data(){
      return{
        weight:null,
        height:null,
        age:null,
        result:null,
        bmiCategory:null,
        bmiTable:[
          {
            name:'Less than 16.0',
            categories:'Severely Underweight'
          },
          {
            name:'16.0 - 18.4',
            categories:'Underweight'
          },
          {
            name:'18.5 - 24.9',
            categories:'Normal'
          },
          {
            name:'25.0 - 29.9',
            categories:'Overweight'
          },
          {
            name:'30.0 - 34.9',
            categories:'Moderately Obese'
          },
          {
            name:'35.0 - 39.9',
            categories:'Severely Obese'
          },
          {
            name:'> 40.0',
            categories:'Morbidly Obese'
          },
        ],
        icons: [
        'mdi-facebook',
        'mdi-twitter',
        'mdi-linkedin',
        'mdi-instagram',
      ]
      }
    },
    props: {
      msg: String
    },
    methods:{
      getValue(){
        console.log("Age:",this.age,"Height:",this.height,"Weight:",this.weight);
        this.bmiCalulator(this.age,this.height,this.weight);
      },
      bmiCalulator(age,height,weight){
        var meterHeight = height * 0.01;
        const squareHeight= meterHeight * meterHeight;
        const Calculate = weight / squareHeight;
        this.result = Calculate;
        // console.log(Calculate);
        this.bmiCategory = this.bmiChart(Calculate);
        // console.log(this.bmiCategory);
        
      },
      bmiChart(bmi){
        if (bmi < 16.0) return "Severely Underweight";
        if (bmi >= 16.0 && bmi <= 18.4) return "Underweight";
        if (bmi >= 18.5 && bmi <= 24.9) return "Normal";
        if (bmi >= 25.0 && bmi <= 29.9) return "Overweight";
        if (bmi >= 30.0 && bmi <= 34.9) return "Moderately Obese";
        if (bmi >= 35.0 && bmi <= 39.9) return "Severely Obese";
        if (bmi >= 40.0) return "Morbidly Obese";
        return "Unknown";
      },
      getHoverCategory(Category){
        if(Category === this.bmiCategory){
          switch(Category){
            case "Severely Underweight": return "severely-underweight";
            case "Underweight": return "underweight";
            case "Normal": return "normal";
            case "Overweight": return "overweight";
            case "Moderately Obese": return "moderately-obese";
            case "Severely Obese": return "severely-obese";
            case "Morbidly Obese": return "morbidly-obese";
          }
        }
        return "";
      }

    }
  }
  </script>
<style>
/* Different Colors for Each BMI Category */
.severely-underweight {
  background-color: #ff9999; /* Light Red */
  font-weight: bold;
  border: 2px black solid;
}
.underweight {
  background-color: #ffcc99; /* Orange */
  font-weight: bold;
}
.normal {
  background-color: #99ff99; /* Green */
  font-weight: bold;
}
.overweight {
  background-color: #ffff99; /* Yellow */
  font-weight: bold;
}
.moderately-obese {
  background-color: #ff9966; /* Dark Orange */
  font-weight: bold;
}
.severely-obese {
  background-color: #ff6666; /* Red */
  font-weight: bold;
}
.morbidly-obese {
  background-color: #cc0000; /* Dark Red */
  color: white;
  font-weight: bold;
}
</style>
  
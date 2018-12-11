<template>
  <div class="calculator">
     <b-form @submit="onSubmit" @reset="onReset" v-if="show">
      <div class="header__form">
        <h1 class="main__header">Сделайте рассчет индивидуальной сауны</h1>
      </div>
      <div class="body__form">
        <div class="column__form">
          <b-form-group id="classSaun"
                    label="Выберите класс сауны:"
                    label-for="classSaun">
            <b-form-select id="classSaun"
                        :options="classSauni"
                        required
                        v-model="form.classSauni">
            </b-form-select>
          </b-form-group>
          <b-form-group id="interiorLining"
                    label="Внутренняя обшивка:"
                    label-for="interiorLining">
            <b-form-select id="interiorLining"
                        :options="interiorLining"
                        required
                        v-model="form.interiorLining">
            </b-form-select>
          </b-form-group>
        </div>
        <div class="column__form">
          <b-form-group id="size"
                    label="Размеры"
                    label-for="size">
            <b-form-input id="width" class="inputsize"
                      type="number"
                      v-model="form.width"
                      required
                      placeholder="Ширина">
            </b-form-input>
            <b-form-input id="height" class="inputsize"
                      type="number"
                      v-model="form.height"
                      required
                      placeholder="Высота">
            </b-form-input>
            <b-form-input id="long" class="inputsize"
                      type="number"
                      v-model="form.long"
                      required
                      placeholder="Длина">
            </b-form-input>
          </b-form-group>
        </div>
        <div class="column__form">
          <b-form-group id="people"
                    label="Вместимость:"
                    label-for="people">
            <span>{{form.people}}</span>
            <span> человек</span>
            <b-form-input id="people" class="inputsize"
                      type="range"
                      v-model="form.people"
                      min="0" max="5">
            </b-form-input>
          </b-form-group>
          <b-form-group>
            <b-form-group id="lights"
                      label="Освещение"
                      label-for="lights">
              <span>{{form.lights}}</span>
              <span> светильников</span>
              <b-form-input id="lights" class="inputsize"
                        type="range"
                        v-model="form.lights"
                        min="0" max="5">
              </b-form-input>
            </b-form-group>
          </b-form-group>
        </div>
      </div>
      <div class="form__footer">
        <div class="column__form">
            <p class="info">Внутрення обшивка: {{this.form.interiorLining}}</p>
            <p class="info">Размер: {{this.form.width}}x{{this.form.height}}x{{this.form.long}}</p>
             <p class="info">Вместимость: {{this.form.people}} человек</p>
              <p class="info">Освещение: {{this.form.lights}} светильников</p>
        </div>
        <div class="column__form">
                    <b-form-group id="size"
                    label="Размеры"
                    label-for="size">
            <b-form-input id="width" class="inputsize"
                      type="text"
                      v-model="form.width"
                      required
                      placeholder="Ширина">
            </b-form-input>
            <b-form-input id="height" class="inputsize"
                      type="text"
                      v-model="form.height"
                      required
                      placeholder="Высота">
            </b-form-input>
          </b-form-group>

        <b-button type="submit" variant="primary">Submit</b-button>
        </div>
      </div>

<!--             <b-form-group id="exampleInputGroup1"
                    label="Email address:"
                    label-for="exampleInput1"
                    description="We'll never share your email with anyone else.">
        <b-form-input id="exampleInput1"
                      type="email"
                      v-model="form.email"
                      required
                      placeholder="Enter email">
        </b-form-input>
      </b-form-group>
      <b-form-group id="exampleInputGroup2"
                    label="Your Name:"
                    label-for="exampleInput2">
        <b-form-input id="exampleInput2"
                      type="text"
                      v-model="form.name"
                      required
                      placeholder="Enter name">
        </b-form-input>
      </b-form-group>
      <b-form-group id="exampleGroup4">
        <b-form-checkbox-group v-model="form.checked" id="exampleChecks">
          <b-form-checkbox value="me">Check me out</b-form-checkbox>
          <b-form-checkbox value="that">Check that out</b-form-checkbox>
        </b-form-checkbox-group>
      </b-form-group>
      <b-button type="submit" variant="primary">Submit</b-button>
      <b-button type="reset" variant="danger">Reset</b-button> -->
    </b-form>
  </div>
</template>

<script>
export default {
  name: 'Calculator',
  data () {
    return {
      form: {
        email: '',
        name: '',
        width: 250,
        height: 270,
        long: 370,
        people: 2,
        lights: 2,
        classSauni: 'Люкс',
        interiorLining: 'Дуб',
        checked: []
      },
      classSauni: [
        { text: 'Люкс', value: 'Люкс' },
        'Эконом', 'Стандарт', 'Люкс', 'Премиум'
      ],
      interiorLining: [
        { text: 'Дуб', value: 'Дуб' },
        'Ольха', 'Сосна', 'Дуб'
      ],
      show: true
    }
  },
  methods: {
    onSubmit (evt) {
      evt.preventDefault()
      alert(JSON.stringify(this.form))
    },
    onReset (evt) {
      evt.preventDefault()
      /* Reset our form values */
      this.form.email = ''
      this.form.name = ''
      this.form.width = 250
      this.form.height = 270
      this.form.long = 310
      this.form.people = ''
      this.form.lights = ''
      this.form.classSauni = 'Люкс'
      this.form.interiorLining = 'Дуб'
      this.form.checked = []
      /* Trick to reset/clear native browser form validation state */
      this.show = false
      this.$nextTick(() => { this.show = true })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
  .calculator{
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
    width: 85%;
    padding: 50px;
    background-image: radial-gradient(circle 531px at 59px 147px,rgb(88, 55, 255) 0%,rgb(11, 72, 175) 40.1%,rgb(78, 110, 157) 100%);
  }
  .header__form{
    margin-bottom: 25px;
  }
  .main__header{
    text-align: center;
    color: white;
    font-size: 25px;
  }

  .body__form{
    display:flex;
    flex-direction: row;
    flex-basis: 1;
    justify-content: center;
    align-content: space-around;
  }
  .form__footer{
    display:flex;
    flex-direction: row;
    flex-basis: 50%;
    justify-content: space-between;

  }
  .column__form{
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    margin-right: 25px;
  }

  .column__form:last-child{
    margin-right: 0px;
  }
  .custom-select{
    background-image: url(data:image/svg+xml;utf8;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iaXNvLTg4NTktMSI/Pgo8IS0tIEdlbmVyYXRvcjogQWRvYmUgSWxsdXN0cmF0b3IgMTguMS4xLCBTVkcgRXhwb3J0IFBsdWctSW4gLiBTVkcgVmVyc2lvbjogNi4wMCBCdWlsZCAwKSAgLS0+CjxzdmcgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIiB4bWxuczp4bGluaz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94bGluayIgdmVyc2lvbj0iMS4xIiBpZD0iQ2FwYV8xIiB4PSIwcHgiIHk9IjBweCIgdmlld0JveD0iMCAwIDEyNS4zMDQgMTI1LjMwNCIgc3R5bGU9ImVuYWJsZS1iYWNrZ3JvdW5kOm5ldyAwIDAgMTI1LjMwNCAxMjUuMzA0OyIgeG1sOnNwYWNlPSJwcmVzZXJ2ZSIgd2lkdGg9IjE2cHgiIGhlaWdodD0iMTZweCI+CjxnPgoJPGc+CgkJPHBvbHlnb24gcG9pbnRzPSI2Mi42NTIsMTAzLjg5NSAwLDIxLjQwOSAxMjUuMzA0LDIxLjQwOSAgICIgZmlsbD0iI2Q2ZDRkNiIvPgoJPC9nPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+Cjwvc3ZnPgo=);
    background-repeat:no-repeat;
  }
  .b-form-group label{
    padding-bottom: 15px;
  }

  .inputsize{
    margin-bottom: 40px;
  }
  .inputsize:last-child{
    margin-bottom: 0px;
  }

  input::-webkit-outer-spin-button,
  input::-webkit-inner-spin-button {
      /* display: none; <- Crashes Chrome on hover */
      -webkit-appearance: none;
      margin: 0; /* <-- Apparently some margin are still there even though it's hidden */
  }
  .form-control{
    font-weight: bold;
  }
  .form-control:focus{
    outline:none;
    border: none;
    box-shadow: none;
  }
</style>

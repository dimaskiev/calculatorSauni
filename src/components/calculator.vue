<template>
  <div class="calculator">
     <b-form @submit="onSubmit" @reset="onReset" v-if="show" class="form">
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
            <div class="size">
              <b-form-input id="width" class="inputsize"
                      type="number"
                      v-model="form.width"
                      required
                      placeholder="Ширина">
              </b-form-input>
              <span>Ширина, см</span>
            </div>
            <div class="size">
            <b-form-input id="long" class="inputsize"
                      type="number"
                      v-model="form.long"
                      required
                      placeholder="Длина">
            </b-form-input>
            <span>Длина, см</span>
            </div>
            <div class="size">
              <b-form-input id="height" class="inputsize"
                      type="number"
                      v-model="form.height"
                      required
                      placeholder="Высота">
            </b-form-input>
            <span>Высота, см</span>
            </div>
          </b-form-group>
        </div>
        <div class="column__form">
          <b-form-group id="people"
                    label="Вместимость:"
                    label-for="people">
            <span>{{form.people}}</span>
            <span> человек</span>
            <b-form-input id="people" class="range__input"
                      type="range"
                      v-model="form.people"
                      min="0" max="12">
            </b-form-input>
          </b-form-group>
          <b-form-group>
            <b-form-group id="lights"
                      label="Освещение"
                      label-for="lights">
              <span>{{form.lights}}</span>
              <span> светильников</span>
              <b-form-input id="lights" class="range__input"
                        type="range"
                        v-model="form.lights"
                        min="0" max="8">
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
        <div class="column__form column__contact">
                    <b-form-group id="contact">
                      <b-form-input id="name" class="input-contact"
                        type="text"
                        v-model="form.name"
                        required
                        placeholder="Имя">
                      </b-form-input>
                    <b-form-input id="tel" class="input-contact"
                      type="text"
                      v-model="form.tel"
                      required
                      placeholder="Телефон">
                    </b-form-input>
          </b-form-group>

        <b-button type="submit" variant="primary">Submit</b-button>
        </div>
      </div>
    </b-form>
    <div>{{result}}</div>
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
        interiorLining: 'Ольха',
        priceSauni: [[3310, 5200, 6300, 7200], [3120, 5050, 6070, 7050], [2930, 4900, 5840, 6900]],
        checked: []
      },
      classSauni: [
        { text: 'Люкс', value: 'Люкс' },
        'Эконом', 'Стандарт', 'Премиум'
      ],
      interiorLining: [
        { text: 'Ольха', value: 'Ольха' },
        'Липа', 'Кедр'
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
      this.form.interiorLining = 'Ольха'
      this.form.priceSauni = 0
      this.form.checked = []
      /* Trick to reset/clear native browser form validation state */
      this.show = false
      this.$nextTick(() => { this.show = true })
    }
  },
  computed: {
    result: function () {
      let size = (this.form.width / 100 * this.form.long / 100).toFixed(2)
      if (size >= 5 && size <= 8) {
        switch (this.form.classSauni) {
          case 'Эконом':
            size *= this.form.priceSauni[0][0]
            break
          case 'Стандарт':
            size *= this.form.priceSauni[0][1]
            break
          case 'Люкс':
            size *= this.form.priceSauni[0][2]
            break
          case 'Премиум':
            size *= this.form.priceSauni[0][3]
            break
        }
      } else {
        if (size >= 9 && size <= 12) {
          switch (this.form.classSauni) {
            case 'Эконом':
              size *= this.form.priceSauni[1][0]
              break
            case 'Стандарт':
              size *= this.form.priceSauni[1][1]
              break
            case 'Люкс':
              size *= this.form.priceSauni[1][2]
              break
            case 'Премиум':
              size *= this.form.priceSauni[1][3]
              break
          }
        } else {
          switch (this.form.classSauni) {
            case 'Эконом':
              size *= this.form.priceSauni[2][0]
              break
            case 'Стандарт':
              size *= this.form.priceSauni[2][1]
              break
            case 'Люкс':
              size *= this.form.priceSauni[2][2]
              break
            case 'Премиум':
              size *= this.form.priceSauni[2][3]
              break
          }
        }
      }
      switch (this.form.interiorLining) {
        case 'Липа':
          size *= 2.5
          break
        case 'Кедр':
          size *= 4.2
          break
        case 'Ольха':
          size *= 3
          break
      }

      if (this.form.lights > 5) size += 1500
      if (this.form.people > 3) size += 2000
      return size
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
    padding: 35px;
    background-image: radial-gradient(circle 531px at 59px 147px,rgb(88, 55, 255) 0%,rgb(11, 72, 175) 40.1%,rgb(78, 110, 157) 100%);
  }

  .form{
    width: 100%;
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
    justify-content: center;
    align-content: space-around;
    margin-bottom: 25px;
  }
  .form__footer{
    display:flex;
    flex-direction: row;
    flex-basis: 50%;
    justify-content: space-between;
    margin: 20px;
    border-radius: 3px;
  }
  .column__form{
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-content: center;
    margin-right: 25px;
    flex-basis: 25%;
  }

  .column__form:first-child{
    flex-basis: 30%;
  }

  .column__form:last-child{
    margin-right: 0px;
    flex-basis: 35%;
  }
  .custom-select{
    background-image: url(data:image/svg+xml;utf8;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iaXNvLTg4NTktMSI/Pgo8IS0tIEdlbmVyYXRvcjogQWRvYmUgSWxsdXN0cmF0b3IgMTguMS4xLCBTVkcgRXhwb3J0IFBsdWctSW4gLiBTVkcgVmVyc2lvbjogNi4wMCBCdWlsZCAwKSAgLS0+CjxzdmcgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIiB4bWxuczp4bGluaz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94bGluayIgdmVyc2lvbj0iMS4xIiBpZD0iQ2FwYV8xIiB4PSIwcHgiIHk9IjBweCIgdmlld0JveD0iMCAwIDEyNS4zMDQgMTI1LjMwNCIgc3R5bGU9ImVuYWJsZS1iYWNrZ3JvdW5kOm5ldyAwIDAgMTI1LjMwNCAxMjUuMzA0OyIgeG1sOnNwYWNlPSJwcmVzZXJ2ZSIgd2lkdGg9IjE2cHgiIGhlaWdodD0iMTZweCI+CjxnPgoJPGc+CgkJPHBvbHlnb24gcG9pbnRzPSI2Mi42NTIsMTAzLjg5NSAwLDIxLjQwOSAxMjUuMzA0LDIxLjQwOSAgICIgZmlsbD0iI2Q2ZDRkNiIvPgoJPC9nPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+CjxnPgo8L2c+Cjwvc3ZnPgo=);
    background-repeat:no-repeat;
  }
  .b-form-group label{
    padding-bottom: 15px;
  }

  .inputsize{
    /* margin-bottom: 30px;*/
    max-width: 100px;
    height: 50px;
    text-align: center;
    margin-right: 15px;
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

  .form__footer{
    color: black;
    background-color: #fff;
    padding: 35px;
  }

   .form__footer .column__form:last-child{
    flex-basis: 50%;
  }

  .info{
    padding: 0;
    margin: 0;
  }

  .size{
    display: flex;
    flex-direction: row;
    align-items: center;
    margin-bottom: 25px;
  }
  .size:last-child{
    margin-bottom: 0px;
  }

</style>

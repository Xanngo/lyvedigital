// Tengo que hacer onReset cuando se haga 'back' en el padre
<template>
  <div class="order-form-component">
      <b-form @submit="onSubmit" @reset="onReset" v-if="show">
        <div class="mandatory-fields">
          <b-form-group
            id="input-group-source"
            label="source"
            label-for="input-source"
          >
            <b-form-input
              id="input-source"
              v-model="form.source"
              type="text"
              required
              :placeholder="sourcePlaceholder"
            ></b-form-input>
          </b-form-group>

          <b-form-group id="input-group-instructions" label="instructions" label-for="input-instructions">
            <b-form-textarea
              id="input-instructions"
              v-model="form.instructions"
              required
              :placeholder="instructionsPlaceholder"
              rows="2"
              no-resize
            ></b-form-textarea>
          </b-form-group>

          <b-row class="writers-and-budget">
            <b-col>
              <b-form-group
                id="input-group-writers"
                label="number of writers"
                label-for="input-writers"
              >
                <b-form-select
                  id="input-writers"
                  v-model="form.writers"
                  required
                  :placeholder="numberWritersPlaceholder"
                  :options="writersOptions"
                ></b-form-select>
              </b-form-group>
            </b-col>
            <b-col>
              <b-form-group
                id="input-group-budget"
                label="budget (USD)"
                label-for="input-budget"
              >
                <b-input-group prepend="$">
                  <b-form-input
                    id="input-budget"
                    v-model="form.budget"
                    type="text"
                    required
                    :placeholder="budgetPlaceholder"
                  ></b-form-input>
                </b-input-group>
              </b-form-group>
            </b-col>
          </b-row>
        </div>
        <div class="optional-fields">
          <div class="select-option">
            Please select options (optional)
          </div>
          <b-form-checkbox-group class="options" v-model="form.options" name="options">
            <b-container fluid>
              <b-row class="option" v-for="option in options" :key="option.id">
                <b-col>{{ option.name }}</b-col>
                <b-col class="increase">(add {{ optionIncementLabel(option) }})</b-col>
                <b-col cols="1">
                  <b-form-checkbox
                    :value="option"
                  />
                </b-col>
              </b-row>
            </b-container>
          </b-form-checkbox-group>
        </div>
        <b-button class="submit" type="submit" variant="primary">
              <div class="shopping-cart">
                <i class="fa fa-shopping-cart" aria-hidden="true"></i>
              </div>
                Submit
              <div class="total-budget">
                $ {{ totalBuget }}
              </div>
        </b-button>
    <!--    <b-button type="reset" variant="danger">Reset</b-button> -->
      </b-form>
    </div>
</template>

<script>
  const getPlaceholder = function(orderDetails, name) {
    return orderDetails.find(element => element.name == name).placeholder;
  }

  export default {
    name: 'order-form-component',
    props: {
      "order-details": Array,
      "options": Array
    },
    data() {
      const writerOptions = Array(15).fill(null).map((value, index) => ({ value: index + 1, text: index + 1 }));
      writerOptions.unshift({ value: null, text: 'select' });

      return {
        form: {
          source: '',
          instructions: '',
          writers: null,
          options: [],
          budget: null
        },
        show: true,
        writersOptions: writerOptions
      }
    },
    computed: {
      sourcePlaceholder() {
        return getPlaceholder(this.orderDetails, "source");
      },
      instructionsPlaceholder() {
        return getPlaceholder(this.orderDetails, "instructions");
      },
      numberWritersPlaceholder() {
        return getPlaceholder(this.orderDetails, "number_writers");
      },
      budgetPlaceholder() {
        return getPlaceholder(this.orderDetails, "budget");
      },
      totalBuget() {
        if (this.form.budget === null || this.form.writers == null) {
          return "-";
        } else {

          let totalBudget = this.form.budget * parseInt(this.form.writers);

          totalBudget = this.form.options.reduce( (totalBudget, option) => {
            return totalBudget * (option.increase ? parseInt(option.increase)/100 + 1 : 1)
              + (option.price ? parseInt(option.price) : 0);
          }, totalBudget);

          return totalBudget.toFixed(2);

        }
      }
    },
    methods: {
      optionIncementLabel(option) {
        if (option.increase) {
          return option.increase + "%";
        } else if (option.price) {
          return "$" + option.price
        }
      },
      onSubmit(evt) {
        evt.preventDefault()
        alert(JSON.stringify(this.form))
      },
      onReset(evt) {
        evt.preventDefault()
        // Reset our form values
        this.form.source = ''
        this.form.instructions = ''
        // Trick to reset/clear native browser form validation state
        this.show = false
        this.$nextTick(() => {
          this.show = true
        })
      }
    }
  }
</script>

<style>
  @import "../assets/lib/fontawesome/css/fontawesome.min.css";
  @import "../assets/lib/fontawesome/css/solid.min.css";

  .order-form-component {
    font-size: 0.8em;
    padding-top: 0.5rem;
    font-weight: 300;
  }
  .order-form-component .mandatory-fields {
    padding-left: 0.5rem;
    padding-right: 1rem;
    padding-bottom: 1rem;
  }

  .order-form-component .form-group {
    margin-bottom: 0.4rem;
  }
  .order-form-component label {
    margin-bottom: 0.2rem;
  }
  .order-form-component .form-control,
  .order-form-component .custom-select,
  .order-form-component .input-group-text {
    font-size: 0.8em;
    border: none;
    background-color: #f8f8fa;
    padding: 0.1rem 0.5rem;
    height: calc(1.5em + 0.5rem + 2px);
  }
  .order-form-component textarea.form-control {
    height: auto;
    padding: 0.4rem 0.5rem;
  }
  .order-form-component .form-control::placeholder {
    color: #b9b8bd;
  }

  .row.writers-and-budget {
    margin-right: 0;
    margin-left: -17px;
    margin-top: 0.7rem;
  }
  .row.writers-and-budget .col {
    padding-right: 0px;
    padding-left: 17px;
  }

  .select-option {
    font-size: 0.6em;
    font-weight: 500;
    padding: 0.9em;
    background-color: #e5e5e5;
  }

  .options .container-fluid {
    font-size: 0.9em;
    padding: 0;
  }
  .options .option {
    padding-top: 0.8rem;
    margin: 0;
    padding-left: 0.5rem;
    padding-right: 1.5rem;
    border-top: 1px solid #fcfcfc;
    border-bottom: 1px solid #f8f8f8;
  }
  .options .option:first-child {
    border-top: none;
  }
  .options .option:last-child {
    border-bottom: none;
  }
  .options .option .col,
  .options .option .col-1 {
    padding: 0;
  }

  .options .option .custom-checkbox .custom-control-label::before {
    border-radius:100%;
    top: 0.15rem;
    left: -1.2rem;
    width: 0.7rem;
    height: 0.7rem;
    border: #000000 solid 2px;
  }

  .options .option .custom-checkbox .custom-control-input:checked ~ .custom-control-label::after {
    background-image: none;
  }

  .options .option .increase {
    color: #b1b1b3;
  }

  .btn.submit {
    width: 90%;
    margin: auto;
    margin-top: 1.2rem;
    display: block;
    border-radius: 8px;
    background-color: #2b62fe;
    text-transform: uppercase;
    font-weight: 800;
    letter-spacing: 0.1em;
  }

  .btn.submit .shopping-cart {
    float: left;
  }

  .btn.submit .total-budget {
    float: right;
    font-size: 0.8em;
    padding-top: 2px;
  }


</style>
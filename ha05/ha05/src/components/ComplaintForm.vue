<template>
  <!-- TODO: implement me -->
  <img src="@/assets/overview.jpg" class="img-fluid rounded" alt="" />
  <form class="needs-validation" novalidate>
    <div class="card" id="main-card">
      <div class="card-body">
        <h5 class="card-title">Complaint form</h5>
        <h6 class="card-subtitle text-muted">
          Flight got canceled? Luggage lost? Get a refund!
        </h6>
        <hr />
        <div class="row">
          <div class="col-6">
            <label for="flight-number" class="form-label">Flight number</label>
            <div class="input-group">
              <input
                type="text"
                class="form-control"
                id="flight-number"
                placeholder="LH0001, LH 0001, LH 1"
                v-model="flightNumber"
                :class="{
                  'is-invalid': isFlightNumberInvalid,
                  'is-valid': isFlightNumberValid,
                }"
                required
              />
              <span class="input-group-text" style="font-size: 12px">123</span>
            </div>
          </div>
          <div class="col-6 input-field">
            <label for="email-address" class="form-label">Email address</label>
            <div class="input-group">
              <input
                type="email"
                class="form-control"
                id="email-address"
                placeholder="muster@tu-berlin.de"
                v-model="emailAddress"
                :class="{
                  'is-invalid': isEmailAddressInvalid,
                  'is-valid': isEmailAddressValid,
                }"
                required
              />
              <span class="input-group-text"
                ><i class="bi bi-envelope"></i
              ></span>
            </div>
          </div>
          <div class="col-6 input-field">
            <label for="flight-date" class="form-label">Date of flight</label>
            <input
              type="date"
              class="form-control"
              id="flight-date"
              required
              v-model="flightDate"
              :class="{
                'is-invalid': isDateInvalid,
                'is-valid': isDateValid,
              }"
            />
          </div>
          <div class="col-6 input-field">
            <label for="flight-time" class="form-label">Time of flight</label>
            <input
              type="time"
              class="form-control"
              id="flight-time"
              required
              v-model="flightTime"
              :class="{
                'is-invalid': isTimeInvalid,
                'is-valid': isTimeValid,
              }"
            />
          </div>
          <div class="col-12 input-field">
            <label for="bank-iban" class="form-label">IBAN</label>
            <div class="input-group">
              <input
                type="text"
                class="form-control"
                id="bank-iban"
                placeholder="DE18 1111 1111 1111 1111 11, DE62 9999 9999 9999 9999 99"
                v-model="bankIban"
                required
                :class="{
                  'is-invalid': isIbanInvalid,
                  'is-valid': isIbanValid,
                }"
              />
              <span class="input-group-text"><i class="bi bi-coin"></i></span>
            </div>
          </div>
        </div>
        <hr />
        <button
          type="button"
          class="btn btn-primary float-end"
          @click="submitForm"
        >
          <i class="bi bi-send-fill"></i>
          Submit complaint
        </button>
      </div>
    </div>
  </form>
</template>

<script>
export default {
  name: "ComplaintForm",
  data() {
    return {
      formSubmitted: false,
      flightNumber: "",
      flightNumberPattern:
        /^([A-Z]{1}[A-Z\d]{1}|[A-Z\d]{1}[A-Z]{1}) ?[\d]{1,4}$/,
      emailAddress: "",
      emailAddressPattern:
        /^([A-z\d]+\.)*[A-z\d]*@(mailbox\.|campus\.){0,1}tu-berlin\.de$/,
      flightDate: "",
      flightDatePattern: /^\d{1,4}-(0?[1-9]|1[012])-(0?[1-9]|[12][0-9]|3[01])$/,
      flightTime: "",
      flightTimePattern: /^([0-1]?[0-9]|2[0-3]):[0-5][0-9]$/,
      bankIban: "",
      bankIbanPattern:
        /^DE[0-9]{2}(?:[ ]?[0-9]{4}){4}(?!(?:[ ]?[0-9]){3})(?:[ ]?[0-9]{1,2})?$/,
    };
  },
  computed: {
    isFlightNumberValid() {
      return this.flightNumberValid(this.flightNumber);
    },
    isFlightNumberInvalid() {
      return this.formSubmitted && !this.flightNumberValid(this.flightNumber);
    },
    isEmailAddressValid() {
      return this.emailAddressValid(this.emailAddress);
    },
    isEmailAddressInvalid() {
      return this.formSubmitted && !this.emailAddressValid(this.emailAddress);
    },
    isDateValid() {
      return this.dateValid(this.flightDate);
    },
    isDateInvalid() {
      return this.formSubmitted && !this.dateValid(this.flightDate);
    },
    isTimeValid() {
      return this.timeValid(this.flightTime);
    },
    isTimeInvalid() {
      return this.formSubmitted && !this.timeValid(this.flightTime);
    },
    isIbanValid() {
      return this.ibanValid(this.bankIban);
    },
    isIbanInvalid() {
      return this.formSubmitted && !this.ibanValid(this.bankIban);
    },
  },
  methods: {
    submitForm() {
      console.log("FORM SUBMITTED");
      this.formSubmitted = true;
    },
    flightNumberValid(value) {
      return value !== "" && this.flightNumberPattern.test(value);
    },
    emailAddressValid(value) {
      return value !== "" && this.emailAddressPattern.test(value);
    },
    dateValid(value) {
      return value !== "" && this.flightDatePattern.test(value);
    },
    timeValid(value) {
      return value !== "" && this.flightTimePattern.test(value);
    },
    ibanValid(value) {
      if (value == "" || !this.bankIbanPattern.test(value)) {
        return false;
      }
      let stringArray = Array.from(value);
      let checksum = parseInt(stringArray[2]) * 10 + parseInt(stringArray[3]);

      return (
        checksum ===
        stringArray
          .slice(4, stringArray.length)
          .filter((char) => char !== " ")
          .reduce((total, char) => total + parseInt(char), 0)
      );
    },
  },
};
</script>

<style scoped>
#main-card {
  background-color: rgba(255, 255, 255, 0.9);
}
.input-field {
  margin-bottom: 20px;
}
</style>
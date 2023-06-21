<script setup lang="ts">
    import { ref } from 'vue'

    const cardNameError = ref("")
    const cardNumberError = ref("")
    const cardExpirationDateError = ref("")

    const cardName = ref("");
    const cardNumber = ref("");
    const cardExpirationMonth = ref("");
    const cardExpirationYear = ref("");
    const cardCvcCode = ref("");

    const cardNameRendering = ref("FULL NAME")
    const cardNumberRendering = ref("#### #### #### ####")
    const cardExpirationMonthRendering = ref("MM")
    const cardExpirationYearRendering = ref("YY")

    function verifyCardName() {
        cardNameError.value = cardName.value.length <= 0 ? "The name on the card cannot be empty" : ""
        if(cardNameError.value.length == 0) {
            cardNameRendering.value = cardName.value
        } else {
            cardNameRendering.value = "FULL NAME"
        }
    }

    function verifyCardNumber() {
        var temp: string = cardNumber.value;
        cardNumberError.value = /^[^0-9]*$/.test(cardNumber.value) ? "The card number must only contains numbers" : cardNumber.value.length != 16 ? "The length of the card code must be of 16" : ""
        if(!/^[^0-9]*$/.test(cardNumber.value)) {
            cardNumberRendering.value = ""
            temp += "#".repeat(16 - temp.length)
            for(let i = 0; i < temp.length; i++) {
                cardNumberRendering.value += ((i % 4 == 0) ? " " : "") + temp.charAt(i)
            }
        } else {
            cardNumberRendering.value = "#### #### #### ####"
        }
    }

    function verifyCvcCode() {

    }

    function verifyCardExpirationDate() {
        const currentDate = new Date()
        if(parseInt(cardExpirationYear.value) < currentDate.getFullYear() || (parseInt(cardExpirationMonth.value) < (currentDate.getMonth() + 1) && parseInt(cardExpirationYear.value) < currentDate.getFullYear())) {
            cardExpirationDateError.value = "Error in the expiration date"
            cardExpirationYearRendering.value = "YY"
            cardExpirationMonthRendering.value = "MM"
        } else {
            cardExpirationDateError.value = ""
            cardExpirationYearRendering.value = cardExpirationYear.value
            cardExpirationMonthRendering.value = cardExpirationMonth.value
        }
    }

</script>

<template>
    <div>
        <div id="cardSample">
            <div id="cardLogo"></div>
            <div id="cardSampleNumber">
                <p>{{ cardNumberRendering }}</p>
            </div>
            <div id="cardBottom">                
                <div id="cardSampleHolderSection">
                    <p class="cardTitle">Card Holder</p>
                    <p>{{ cardNameRendering }}</p>
                </div>
                <div id="cardSampleExpireSection">
                    <p class="cardTitle">Expires</p>
                    <p>{{ cardExpirationMonthRendering }}/{{ cardExpirationYearRendering }}</p>
                </div>
            </div>
        </div>
    </div>
    <form>
        <label for="name">Name on card</label>
        <input type="text" id="name" name="name" v-model="cardName" @keyup="verifyCardName" />
        <span class="error" v-if="cardNameError.length > 0">{{ cardNameError }}</span>
        <label for="cardNumber">Card number</label>
        <input type="text" id="cardNumber" name="cardNumber" v-model="cardNumber" @keyup="verifyCardNumber" />
        <span class="error" v-if="cardNumberError.length > 0">{{ cardNumberError }}</span>
        <div>
            <fieldset>
                <caption>Expiration date</caption>
                <div>
                    <input type="number" min="1" max="12" id="month" name="expirationMonth" placeholder="Month" v-model="cardExpirationMonth" @keyup="verifyCardExpirationDate" />
                    <input type="text" id="year" name="expirationYear" placeholder="Year" v-model="cardExpirationYear" @keyup="verifyCardExpirationDate" />
                </div>
                <span class="error" v-if="cardExpirationDateError.length > 0">{{ cardExpirationDateError }}</span>
            </fieldset>
            <fieldset>
                <caption>CVC</caption>
                <input type="number" id="cvc" name="cvcCode" placeholder="CVC" v-model="cardCvcCode" @input="verifyCvcCode" />
                <span class="error" v-if="cardExpirationDateError.length > 0">{{ cardExpirationDateError }}</span>
            </fieldset>
        </div>
        <button>Confirm payement</button>
    </form>
</template>

<style scoped>
    form {
        width: 65%;
        min-width: 250px;
        display: flex;
        flex-direction: column;
    }
    form > label, fieldset {
        margin-top: 2%;
    }
    form > input, fieldset {
        margin-bottom: 2%;
    }
    caption {
        width: max-content;
    }
    input, label {
        width: 100%;
    }
    form div {
        display: flex;
        flex-direction: row;
    }
    form fieldset:first-child {
        width: 60%;
    }
    form fieldset:nth-child(2) {
        width: 40%;
    }
    .error {
        color: red;
    }
    button {
        height: 35px;
        background: #2c85ce;
        border-radius: 25px;
        color: white;
    }
    #cardSample {
        padding: 4%;
        width: 350px;
        height: 180px;
        display: flex;
        flex-direction: column;
        box-shadow: 2px;
        border: 1px solid #2c85ce;
        border-radius: 25px;
    }
    #cardLogo {
        border-radius: 18px;
        width: 70px;
        height: 50px;
        background: #2c85ce;
    }
    #cardSampleNumber {
        margin-top: 32px;
        margin-bottom: 32px;
    }
    #cardBottom {
        display: flex;
        flex-direction: row;
        justify-content: space-between;
    }
    .cardTitle {
        font-size: 10pt;
    }
    p {
        margin: 0;
    }
</style>
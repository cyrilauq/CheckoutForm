<script setup lang="ts">
    import { ref, watch } from 'vue'

    const cardNameError = ref("")
    const cardNumberError = ref("")
    const cardExpirationDateError = ref("")
    const cardCvcCodeError = ref("")

    const cardName = ref("");
    const cardNumber = ref("");
    const cardExpirationMonth = ref("");
    const cardExpirationYear = ref("");
    const cardCvcCode = ref("");

    const cardNameRendering = ref("FULL NAME")
    const cardNumberRendering = ref("#### #### #### ####")
    const cardExpirationMonthRendering = ref("MM")
    const cardExpirationYearRendering = ref("YY")

    watch(
        cardName,
        verifyCardName
    )

    watch(
        cardNumber,
        verifyCardNumber
    )

    watch(
        cardCvcCode,
        verifyCvcCode
    )

    function verifyCardName() {
        cardNameError.value = cardName.value.length <= 0 ? "The name on the card cannot be empty" : ""
        if(cardNameError.value.length == 0) {
            cardNameRendering.value = cardName.value
        } else {
            cardNameRendering.value = "FULL NAME"
        }
    }

    function verifyCardNumber() {
        cardNumber.value = cardNumber.value.substring(0, 16)
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
        cardExpirationYearRendering.value = "YY"
        cardExpirationMonthRendering.value = "MM"
        const currentYear = currentDate.getFullYear() % 100;
        if(parseInt(cardExpirationMonth.value) < 1 || parseInt(cardExpirationMonth.value) > 12) {
            cardExpirationDateError.value = "The given month isn't valid"
        } else if(parseInt(cardExpirationYear.value) < currentYear || (parseInt(cardExpirationMonth.value) < (currentDate.getMonth() + 1) && parseInt(cardExpirationYear.value) < currentYear)) {
            cardExpirationDateError.value = "Error in the expiration date"
        } else {
            cardExpirationDateError.value = ""
            cardExpirationYearRendering.value = cardExpirationYear.value
            cardExpirationMonthRendering.value = cardExpirationMonth.value
        }
    }

</script>

<template>
    <div id="payementInformation">
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
        <form>
            <label for="name">Name on card</label>
            <input type="text" id="name" name="name" v-model="cardName" />
            <span class="error" v-if="cardNameError.length > 0">{{ cardNameError }}</span>
            <label for="cardNumber">Card number</label>
            <input type="text" id="cardNumber" name="cardNumber" v-model="cardNumber" />
            <span class="error" v-if="cardNumberError.length > 0">{{ cardNumberError }}</span>
            <div>
                <fieldset>
                    <caption>Expiration date</caption>
                    <div>
                        <input type="number" min="1" max="12" id="month" name="expirationMonth" placeholder="Month" v-model="cardExpirationMonth" @keyup="verifyCardExpirationDate" />
                        <input type="number" min="0" max="99" id="year" name="expirationYear" placeholder="Year" v-model="cardExpirationYear" @keyup="verifyCardExpirationDate" />
                    </div>
                    <span class="error" v-if="cardExpirationDateError.length > 0">{{ cardExpirationDateError }}</span>
                </fieldset>
                <fieldset>
                    <caption>CVC</caption>
                    <input type="number" id="cvc" name="cvcCode" placeholder="CVC" v-model="cardCvcCode" />
                    <span class="error" v-if="cardCvcCodeError.length > 0">{{ cardCvcCodeError }}</span>
                </fieldset>
            </div>
            <button>Confirm payement</button>
        </form>
    </div>
</template>

<style scoped>
    #payementInformation {
        min-width: 400px;
    }
    form {
        width: 65%;
        max-width: 500px;
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
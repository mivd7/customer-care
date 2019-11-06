<template>
    <div>
        <div v-if="!showNextStep" class="cc-form">
            <div class="cc-form__header"><b>Welcome!<br/></b><img src="../assets/cc-icon.png" alt="cc-icon" class="cc-form__icon"/></div>
            <p>Please fill out your complete details to continue.</p>
            <div class="cc-form__fields">
                <form @submit="handleSubmit">
                    <input placeholder="First Name" v-model="firstName"/>
                    <input placeholder="Last Name" v-model="lastName"/>
                    <input placeholder="E-mail" v-model="formModel.EMAIL"/>
                    <input placeholder="Registered Phone No." v-model="formModel.phonenumber"/><br/>
                    <a @click="goToNextStep"><div class="cc-form__btn">Next</div></a>
                </form>
            </div>
        </div>
        <div v-else class="cc-form">
            <div class="cc-form__header">
                <b>What's up, {{firstName}}?<br/></b><img src="../assets/cc-icon.png" alt="cc-icon" class="cc-form__icon"/>
            </div>
            <form class="cc-form__fields">
                <br/>
                <textarea name="message" rows="50" cols="30" v-model="formModel.request" placeholder="Tell us..."></textarea>
                <br>
                <span><label>Unsubscribe from our services?</label><input type="checkbox" id="checkbox" v-model="formModel.unsubscribe"><br/></span>
                <a @click="handleSubmit"><div class="cc-form__btn">Submit</div></a>
            </form>
        </div>
        <div v-if="isDone" class="cc-form">
            <div class="cc-form__header"><b>Thank you for your message, {{firstName}}!<br/></b><img src="../assets/cc-icon.png" alt="cc-icon" class="cc-form__icon"/></div>
            <p>We will get back to you as soon as possible (that's usually no more than 3 days...)</p>
        </div>
    </div>
</template>
    
<script>
import axios from 'axios';
import { baseUrl } from '../constants';

export default {
    name: 'Form',
    data() {
      return {
        formModel: {
          EMAIL: '',
          fullname: '',
          phonenumber: '',
          request: '',
          unsubscribe: false,
        },
        firstName: '',
        lastName: '',
        showNextStep: false,
        isDone: false,
        // unsubscribe: false,
      }
    },
    methods: {
        goToNextStep() {
            const { firstName, lastName } = this;
            if (firstName !== '' && lastName !== '') {
                this.formModel.fullname = this.formModel.fullname.concat(firstName, ' ', lastName);
            } else {
                this.formModel.fullname = firstName
            }
            this.showNextStep = true
        },
        handleSubmit() {
            const { EMAIL, fullname, phonenumber, request } = this.formModel;
            if(EMAIL === '' || fullname === '' || phonenumber === '' || request === '') {
                console.warn('not all fields completed!', this.formModel)
            } else {
                this.isDone = true
                this.sendMessage(this.formModel)
            }
        },
        async sendMessage(messageRequest) {
            console.log('sending:', messageRequest)
            await axios.post(`${baseUrl}/sendMail/`, messageRequest)
                       .then(response => console.log('message send!', response.data))
                       .catch(err => console.error('Error sending message!', err))
        },
        reset() {
            location.reload();
        }
    }
}
</script>

<style>
    .cc-form {
        font-size: 1.6rem;
        position: absolute;
        top: 20%;
        left: 40%;
        background-color: white;
        border-radius: 10%;
        height: 500px;
        width: 500px;
        padding: 50px;
        margin: 10px 0;
    }
    .cc-form__header {
        margin-left: 100px;
    }
    .cc-form__icon {
        position: absolute;
        top: 35px;
        left: 50px;
    }
    .cc-form p {
        margin-top: 33px;
        font-size: 1rem;
        color: grey;
    }
    .cc-form__fields .cc-form__btn {
        background-color: #0072bc;
        color: white;
        font-size: 1.6rem;
        padding: 17px;
        margin-top: 25px;
        border-radius: 50px;
    }

    .cc-form__fields form, a {
        width: 100%;
        text-align: center;
        cursor: pointer;
    }

    .cc-form__fields input {
        width: 90%;
		height: 42px;
		margin: 5px 0;
		border: none;
        border-radius: 30px;
        background-color: whitesmoke;
        padding: 12.5px;
        padding-left: 25px;
        font-size: 1.2rem;
        font-weight: 100;
        text-align: left;
    }

    .cc-form__fields input::placeholder {
        color: grey;
        font-size: 1rem;
    }

    .cc-form__fields textarea {
        width: 90%;
        height: 250px;
		border: none;
		border-radius: 30px;
        background-color: whitesmoke;
        padding: 25px;
        font-size: 1rem;
        font-weight: 100;
        text-align: left;
        resize: none;
    }

    .cc-form__fields label {
        font-size: 1rem;
    }
    #checkbox {
        position: absolute;
        bottom: 20.5%;
        left: 50%;
    }
    .cc-form__fields span {
        margin-left: 10px;
    }
</style>
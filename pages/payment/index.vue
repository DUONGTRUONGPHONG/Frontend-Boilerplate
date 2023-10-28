<template>
    <div class="bg-prim-5 payment">
        <div class="xl:flex xl:gap-5 mx-[5%] ">
            <div class="w-full xl:w-2/3 pt-5">
                <div class="w-full bg-white rounded-md border-prim-10 shadow border p-4 mb-5">
                    <h5>Billing cycle</h5>
                    <p>
                        Choose how often you'd like to be billed.
                        You can cancel anytime
                    </p>
                    <div class="w-full bg-white rounded-md border-prim-10 border shadow mt-4">
                        <a-radio-group v-model="valueBilling" class="w-full">
                            <div
                                :class="[valueBilling === 1 ?'bg-prim-10':'',
                                         'w-full flex gap-2 p-4 border-b border-prim-10 items-center rounded-t-md cursor-pointer']"
                                @click="valueBilling=1"
                            >
                                <a-radio :value="1" />
                                <div class="">
                                    <h5>Monthly</h5>
                                    <p>Pay $25/month</p>
                                </div>
                            </div>
                            <div
                                :class="[valueBilling === 2 ?'bg-prim-10':'',
                                         'w-full flex gap-2 p-4 items-center rounded-b-md cursor-pointer']"
                                @click="valueBilling=2"
                            >
                                <a-radio :value="2" />
                                <div class="w-full">
                                    <div class="flex justify-between">
                                        <div class="flex">
                                            <h5>Yearly</h5><a-tag
                                                color="cyan"
                                                style="margin-left: 6px;border-radius: 22px;
                                        padding:0 0.5rem;"
                                            >
                                                Save $72
                                            </a-tag>
                                        </div>
                                        <span class="text-[#26553f]">Save $72</span>
                                    </div>
                                    <span>$19/month - pay $228 ($19 x 12 months)</span>
                                </div>
                            </div>
                        </a-radio-group>
                    </div>
                    <div class="w-full flex justify-end gap-3 mt-4">
                        <a-button>
                            Cancel
                        </a-button>
                        <a-button
                            style="color: white; background-color: rgb(59, 63, 63);
                                 border: none;"
                            type="primary"
                        >
                            Confirm
                        </a-button>
                    </div>
                </div>
                <div class="w-full bg-white rounded-md border-prim-10 shadow border p-4 mb-5">
                    <h5>Business address</h5>
                    <p>
                        Used on customer order confirmations and your
                        Shopify bill
                    </p>
                    <a-form-model
                        ref="formBusiness"
                        class="!mt-4"
                        :model="formBusiness"
                        :rules="rules"
                        layout="vertical"
                    >
                        <a-form-model-item label="Country/region">
                            <a-input value="Vietnam" disabled />
                            <span class="cursor-pointer text-prim-90">Change country/region</span>
                        </a-form-model-item>
                        <div class="flex gap-3">
                            <a-form-model-item label="First name" class="w-1/2" prop="firstName">
                                <a-input v-model="formBusiness.firstName" />
                            </a-form-model-item>
                            <a-form-model-item label="Last name" class="w-1/2" prop="lastName">
                                <a-input v-model="formBusiness.lastName" />
                            </a-form-model-item>
                        </div>
                        <a-form-model-item label="Address" prop="address">
                            <a-input-search v-model="formBusiness.address" />
                        </a-form-model-item>
                        <a-form-model-item label="Apartment, suite, etc.">
                            <a-input value="Vietnam" />
                        </a-form-model-item>
                        <div class="flex gap-3">
                            <a-form-model-item label="City" class="w-1/2">
                                <a-input value="Vietnam" />
                            </a-form-model-item>
                            <a-form-model-item label="Postal code" class="w-1/2">
                                <a-input value="Vietnam" />
                            </a-form-model-item>
                        </div>
                        <a-form-model-item label="Phone" prop="phone">
                            <a-input v-model="formBusiness.phone" />
                        </a-form-model-item>
                        <span>We'll use this if we need to contect you.</span>
                        <a-form-model-item>
                            <div class="w-full flex justify-end gap-3 mt-4">
                                <a-button
                                    style="color: white; background-color: rgb(59, 63, 63);
                                 border: none;"
                                    type="primary"
                                    @click="handleSubmitBusiness"
                                >
                                    Save address
                                </a-button>
                            </div>
                        </a-form-model-item>
                    </a-form-model>
                </div>
                <div class="w-full bg-white rounded-md border-prim-10 shadow border p-4">
                    <div class="flex justify-between">
                        <h5>Payment method</h5>
                        <a-button v-if="!showPayment" @click="showPayment = !showPayment">
                            Add
                        </a-button>
                    </div>
                    <div v-if="showPayment">
                        <span>Choose how you'd like to pay for Shopify</span>
                        <a-radio-group v-model="valuePayment" class="w-full">
                            <div class="w-full bg-white rounded-md border-prim-10 border shadow mt-4">
                                <span
                                    :class="[valuePayment === 1 ?'bg-prim-10':'',
                                             'flex items-center gap-2 p-4 rounded-t-md cursor-pointer']"
                                    @click="valuePayment=1"
                                >
                                    <a-radio :value="1" />
                                    <h5>Credit or debit card</h5></span>
                                <div class="item" :style="{ 'max-height': valuePayment === 1 ? '1500px' : '0' }">
                                    <div class="m-4">
                                        <a-form-model
                                            ref="form"
                                            :model="form"
                                            :rules="rules"
                                            layout="vertical"
                                        >
                                            <h5>Credit card information</h5>
                                            <a-form-model-item label="Card number" prop="cardNumder">
                                                <a-input
                                                    v-model="form.cardNumber"
                                                    class="!pr-9"
                                                />
                                                <a-icon class="absolute right-3 top-1/2 -translate-y-1/2" type="lock" />
                                            </a-form-model-item>
                                            <div class="flex gap-3">
                                                <a-form-model-item label="Expires" class="w-1/2" prop="expires">
                                                    <a-date-picker
                                                        v-model="form.expires"
                                                        placeholder="MM/YY"
                                                        format="MM/YY"
                                                    >
                                                        <template #suffixIcon>
                                                            <a-icon type="info-circle" />
                                                        </template>
                                                    </a-date-picker>
                                                </a-form-model-item>
                                                <a-form-model-item label="CVV" class="w-1/2" prop="cvv">
                                                    <a-input
                                                        v-model="form.cvv"
                                                        value="Vietnam"
                                                    />
                                                </a-form-model-item>
                                            </div>
                                            <h5>Billing address</h5>
                                            <a-form-model-item label="Country/region">
                                                <a-input value="Vietnam" />
                                            </a-form-model-item>
                                            <div class="flex gap-3">
                                                <a-form-model-item label="First name" class="w-1/2" prop="firstName">
                                                    <a-input v-model="form.firstName" />
                                                </a-form-model-item>
                                                <a-form-model-item label="Last name" class="w-1/2" prop="lastName">
                                                    <a-input v-model="form.lastName" />
                                                </a-form-model-item>
                                            </div>
                                            <a-form-model-item label="Address" prop="address">
                                                <a-input-search v-model="form.address" />
                                            </a-form-model-item>
                                            <a-form-model-item label="Apartment, suite, etc.">
                                                <a-input value="Vietnam" />
                                            </a-form-model-item>
                                            <div class="flex gap-3">
                                                <a-form-model-item label="City" class="w-1/2">
                                                    <a-input value="Vietnam" />
                                                </a-form-model-item>
                                                <a-form-model-item label="Postal code" class="w-1/2">
                                                    <a-input value="Vietnam" />
                                                </a-form-model-item>
                                            </div>
                                            <a-form-model-item label="Phone" prop="phone">
                                                <a-input v-model="form.phone" />
                                            </a-form-model-item>
                                            <span>We'll use this if we need to contect you.</span>
                                            <a-form-model-item>
                                                <div class="w-full flex justify-end gap-3 mt-4">
                                                    <a-button
                                                        style="color: white; background-color: rgb(59, 63, 63);
                             border: none;"
                                                        type="primary"
                                                        @click="handleSubmitPayment"
                                                    >
                                                        Pay
                                                    </a-button>
                                                </div>
                                            </a-form-model-item>
                                        </a-form-model>
                                    </div>
                                </div>
                            </div>
                            <div class="w-full bg-white rounded-md border-prim-10 border shadow mt-4">
                                <span
                                    :class="[valuePayment === 2 ?'bg-prim-10':'',
                                             'flex items-center gap-2 p-4 rounded-t-md cursor-pointer']"
                                    @click="valuePayment=2"
                                >
                                    <a-radio :value="2" />
                                    <font-awesome-icon icon="paypal" style="color: #22deec;" />
                                    <span>
                                        <strong class="text-prim-100"><i>Pay</i></strong><strong class="text-prim-90"><i>Pal</i></strong>
                                    </span>
                                </span>
                                <div
                                    :style="{ 'max-height': valuePayment === 2 ? '1000px' : '0' }"
                                    :class="[valuePayment === 2 ?'m-4':'', 'item']"
                                >
                                    <span>Connect your PayPal account and use it to pay your bills. You'll be
                                        redirected to PayPal to add your billing information.</span>
                                    <div class="w-full flex justify-end gap-3 mt-4">
                                        <a-button block style="max-width: 40%;">
                                            Pay with<strong class="text-prim-100"><i>&nbsp;Pay</i></strong><strong class="text-prim-90"><i>Pal</i></strong>
                                        </a-button>
                                    </div>
                                </div>
                            </div>
                        </a-radio-group>
                    </div>
                </div>
            </div>
            <div class="w-full mt-5 xl:w-1/3">
                <div class="w-full bg-white rounded-md border-prim-10 shadow border">
                    <div class="flex justify-between items-center  p-4">
                        <h5>Basic Shopify plan</h5>
                        <span class="cursor-pointer text-prim-90">Change plan</span>
                    </div>
                    <p class=" px-4">
                        You can change or cancel your plan at any time. Prices excl. additional taxes
                    </p>
                    <div class="flex justify-between items-center  p-4 pt-0">
                        <div class="flex gap-2">
                            <a-checkbox indeterminate />
                            <div class="">
                                <h5>Today</h5>
                                <p>Ongoing plan</p>
                            </div>
                        </div>
                        <div class="text-right">
                            <h5>$25.00</h5>
                            <p>billed every 30 day</p>
                        </div>
                    </div>
                    <div
                        class="border-y border-prim-10 flex justify-between p-4 items-center cursor-pointer"
                        @click="showPlandetail=!showPlandetail"
                    >
                        <h5>Plan details</h5>
                        <a-icon v-if="showPlandetail" type="up" />
                        <a-icon v-else type="down" />
                    </div>
                    <div class="item" :style="{ 'max-height': showPlandetail ? '500px' : '0' }">
                        <div class="p-4 bg-prim-5  border-y border-prim-10">
                            <ul style="list-style: inside;">
                                <li><strong>2 staff members</strong></li>
                                <li>Up to <strong>1,000 locations</strong></li>
                                <li>Shipping discounts</li>
                                <li>Shopify POS for markets and events</li>
                            </ul>
                        </div>
                    </div>
                    <div class="p-4">
                        <div class="flex justify-between mb-4">
                            <h5>Total</h5>
                            <h5>$25.00 USD + tax</h5>
                        </div>
                        <a-button block disabled>
                            Subscribe
                        </a-button>
                    </div>
                    <div class="px-4 mb-4">
                        You need to confirm your billing cycle, add a business address,
                        and add a payment method before you can start this plan.
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        auth: false,
        data() {
            return {
                valueBilling: 1,
                valuePayment: 1,
                sidebarVisible: false,
                showPayment: false,
                showPlandetail: true,
                form: {},
                formBusiness: {},
                rules: {
                    phone:
                        [
                            { required: true, message: 'Please input your phone number!' },
                            {
                                pattern: /^0\d{9}$/,
                                message: 'Phone number is in wrong format',
                            },
                        ],
                    address:
                        [
                            { required: true, message: 'Please input your address!' },
                            {
                                pattern: /^(?!.* {2})[^!@#$%^&*()+.=_]{2,}$/g,
                                message: 'Address is in wrong format',
                            },
                        ],
                    lastName:
                        [
                            { required: true, message: 'Please input your Last name!' },
                            {
                                pattern: /^(?!.* {2})[^\d!@#$%^&*()+.=_-]{2,}$/g,
                                message: 'Last name is in wrong format',
                            },
                        ],
                    firstName:
                        [
                            { required: true, message: 'Please input your First name!' },
                            {
                                pattern: /^(?!.* {2})[^\d!@#$%^&*()+.=_-]{2,}$/g,
                                message: 'First name is in wrong format',
                            },
                        ],
                    cvv:
                        [{ required: true, message: 'Please input your CVV!' },
                         { pattern: /^\d{3}$/, message: 'CVV must have length 3' },
                        ],
                    cardNumder:
                        [{ required: true, message: 'Please input your Card number!' },
                         {
                             pattern: /^\d{16}$|^\d{19}$/,
                             message: 'Card number must have a length of 16 or 19',
                         },
                        ],
                    expires:
                        [{ required: true, message: 'Please input your Expires!' }],
                },
            };
        },
        methods: {
            handleSubmitPayment() {
                this.$refs.form.validate((valid) => {
                    if (valid) {
                        console.log('check');
                    }
                });
            },
            handleSubmitBusiness() {
                this.$refs.formBusiness.validate((valid) => {
                    if (valid) {
                        console.log('check');
                    }
                });
            },
        },
    };
</script>

<style lang="scss">
.item{
    overflow: hidden;
  transition: max-height 0.5s ease;
}
.payment p,h5{
    margin: 0 ;
}
</style>

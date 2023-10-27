<template>
    <div class="bg-prim-5">
        <div class="xl:flex xl:gap-5 mx-[5%] ">
            <div class="w-full xl:w-2/3 pt-5">
                <div class="w-full bg-white rounded-md border-prim-10 shadow border p-4 mb-5">
                    <strong>Billing cycle</strong> <br>
                    <span>Choose how often you'd like to be billed.
                        You can cancel anytime</span>
                    <div class="w-full bg-white rounded-md border-prim-10 border shadow mt-4">
                        <a-radio-group v-model="valueBilling" class="w-full">
                            <div
                                :class="[valueBilling === 1 ?'bg-prim-10':'',
                                         'w-full flex gap-2 p-4 border-b border-prim-10 items-center rounded-t-md']"
                            >
                                <a-radio :value="1" />
                                <div class="">
                                    <strong>Monthly</strong> <br>
                                    <span>Pay $25/month</span>
                                </div>
                            </div>
                            <div :class="[valueBilling === 2 ?'bg-prim-10':'','w-full flex gap-2 p-4 items-center rounded-b-md']">
                                <a-radio :value="2" />
                                <div class="w-full">
                                    <div class="flex justify-between">
                                        <strong>Yearly<a-tag
                                            color="cyan"
                                            style="margin-left: 6px;border-radius: 22px;
                                        padding:0 0.5rem;"
                                        >
                                            Save $72
                                        </a-tag></strong>
                                        <span class="text-[#26553f]">Save $72</span>
                                    </div>
                                    <span>$19/month - pay $228 ($19 x 12 months)</span>
                                </div>
                            </div>
                        </a-radio-group>
                    </div>
                    <div class="w-full flex justify-end gap-3 mt-4">
                        <!-- <button class="rounded-md border-prim-10 border shadow px-2 py-1 flex justify-center items-center">
                            Cancel
                        </button>
                        <button class="rounded-md border-prim-10 border shadow px-2 py-1 bg-gray-100 text-white">
                            Confirm
                        </button> -->
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
                    <strong>Business address</strong> <br>
                    <span>Used on customer order confirmations and your
                        Shopify bill</span>
                    <a-form
                        class="!mt-4"
                        :form="formBusiness"
                        layout="vertical"
                        @submit="handleSubmitBusiness"
                    >
                        <a-form-item label="Country/region">
                            <a-input value="Vietnam" disabled />
                            <span class="cursor-pointer text-[#4185de]">Change country/region</span>
                        </a-form-item>
                        <div class="flex gap-3">
                            <a-form-item label="First name" class="w-1/2">
                                <a-input
                                    v-decorator="[
                                        'firstName',
                                        { rules: [
                                            { required: true, message: 'Please input your First name!' },
                                            {pattern:/^(?!.* {2})[^\d!@#$%^&*()+.=_-]{2,}$/g,
                                             message:'First name is in wrong format'}
                                        ] },
                                    ]"
                                />
                            </a-form-item>
                            <a-form-item label="Last name" class="w-1/2">
                                <a-input
                                    v-decorator="[
                                        'lastName',
                                        { rules: [
                                            { required: true, message: 'Please input your Last name!' },
                                            {pattern:/^(?!.* {2})[^\d!@#$%^&*()+.=_-]{2,}$/g,
                                             message:'Last name is in wrong format'}
                                        ] },
                                    ]"
                                />
                            </a-form-item>
                        </div>
                        <a-form-item label="Address">
                            <a-input-search
                                v-decorator="[
                                    'address',
                                    { rules: [
                                        { required: true, message: 'Please input your address!' },
                                        {pattern:/^(?!.* {2})[^!@#$%^&*()+.=_]{2,}$/g,
                                         message:'Address is in wrong format'}
                                    ] },
                                ]"
                            />
                        </a-form-item>
                        <a-form-item label="Apartment, suite, etc.">
                            <a-input value="Vietnam" />
                        </a-form-item>
                        <div class="flex gap-3">
                            <a-form-item label="City" class="w-1/2">
                                <a-input value="Vietnam" />
                            </a-form-item>
                            <a-form-item label="Postal code" class="w-1/2">
                                <a-input value="Vietnam" />
                            </a-form-item>
                        </div>
                        <a-form-item label="Phone">
                            <a-input
                                v-decorator="[
                                    'phone',
                                    { rules: [
                                        { required: true, message: 'Please input your phone number!' },
                                        {pattern:/^0\d{9}$/,
                                         message:'Phone number is in wrong format'}
                                    ] },
                                ]"
                            />
                        </a-form-item>
                        <span>We'll use this if we need to contect you.</span>
                        <a-form-item>
                            <div class="w-full flex justify-end gap-3 mt-4">
                                <!-- <button
                                    class="rounded-md border-prim-10 border shadow px-2 py-1
                                 bg-gray-100 text-white"
                                >
                                    Save address
                                </button> -->
                                <a-button
                                    style="color: white; background-color: rgb(59, 63, 63);
                                 border: none;"
                                    html-type="submit"
                                    type="primary"
                                >
                                    Save address
                                </a-button>
                            </div>
                        </a-form-item>
                    </a-form>
                </div>
                <div class="w-full bg-white rounded-md border-prim-10 shadow border p-4">
                    <div class="flex justify-between">
                        <strong>Payment method</strong>
                        <a-button v-if="!showPayment" @click="showPayment = !showPayment">
                            Add
                        </a-button>
                    </div>
                    <div v-if="showPayment">
                        <span>Choose how you'd like to pay for Shopify</span>
                        <a-radio-group v-model="valuePayment" class="w-full">
                            <div class="w-full bg-white rounded-md border-prim-10 border shadow mt-4">
                                <span :class="[valuePayment === 1 ?'bg-prim-10':'','flex items-center gap-2 p-4 rounded-t-md']">
                                    <a-radio :value="1" />
                                    <strong>Credit or debit card</strong></span>
                                <div v-if="valuePayment === 1" class="m-4">
                                    <a-form
                                        :form="form"
                                        layout="vertical"
                                        @submit="handleSubmitPayment"
                                    >
                                        <strong>Credit card information</strong>
                                        <a-form-item label="Card number">
                                            <a-input
                                                v-decorator="[
                                                    'cardNumder',
                                                    { rules: [{ required: true, message: 'Please input your Card number!' },
                                                              {pattern:/^\d{16}$|^\d{19}$/,
                                                               message:'Card number must have a length of 16 or 19'}
                                                    ] },
                                                ]"
                                                class="!pr-9"
                                            />
                                            <a-icon class="absolute right-3 top-1/2 -translate-y-1/2" type="lock" />
                                        </a-form-item>
                                        <div class="flex gap-3">
                                            <a-form-item label="Expires" class="w-1/2">
                                                <a-date-picker
                                                    v-decorator="[
                                                        'expires',
                                                        { rules: [{ required: true, message: 'Please input your Expires!' }] },
                                                    ]"
                                                    placeholder="MM/YY"
                                                    format="MM/YY"
                                                >
                                                    <template #suffixIcon>
                                                        <a-icon type="info-circle" />
                                                    </template>
                                                </a-date-picker>
                                            </a-form-item>
                                            <a-form-item label="CVV" class="w-1/2">
                                                <a-input
                                                    v-decorator="[
                                                        'cvv',
                                                        { rules: [{ required: true, message: 'Please input your CVV!' },
                                                                  { pattern:/^\d{3}$/, message: 'CVV must have length 3' }
                                                        ] },
                                                    ]"
                                                    value="Vietnam"
                                                />
                                            </a-form-item>
                                        </div>
                                        <strong>Billing address</strong>
                                        <a-form-item label="Country/region">
                                            <a-input value="Vietnam" />
                                        </a-form-item>
                                        <div class="flex gap-3">
                                            <a-form-item label="First name" class="w-1/2">
                                                <a-input
                                                    v-decorator="[
                                                        'firstName',
                                                        { rules: [
                                                            { required: true, message: 'Please input your First name!' },
                                                            {pattern:/^(?!.* {2})[^\d!@#$%^&*()+.=_-]{2,}$/g,
                                                             message:'First name is in wrong format'}
                                                        ] },
                                                    ]"
                                                />
                                            </a-form-item>
                                            <a-form-item label="Last name" class="w-1/2">
                                                <a-input
                                                    v-decorator="[
                                                        'lastName',
                                                        { rules: [
                                                            { required: true, message: 'Please input your Last name!' },
                                                            {pattern:/^(?!.* {2})[^\d!@#$%^&*()+.=_-]{2,}$/g,
                                                             message:'Last name is in wrong format'}
                                                        ] },
                                                    ]"
                                                />
                                            </a-form-item>
                                        </div>
                                        <a-form-item label="Address">
                                            <a-input-search
                                                v-decorator="[
                                                    'address',
                                                    { rules: [
                                                        { required: true, message: 'Please input your address!' },
                                                        {pattern:/^(?!.* {2})[^!@#$%^&*()+.=_]{2,}$/g,
                                                         message:'Address is in wrong format'}
                                                    ] },
                                                ]"
                                            />
                                        </a-form-item>
                                        <a-form-item label="Apartment, suite, etc.">
                                            <a-input value="Vietnam" />
                                        </a-form-item>
                                        <div class="flex gap-3">
                                            <a-form-item label="City" class="w-1/2">
                                                <a-input value="Vietnam" />
                                            </a-form-item>
                                            <a-form-item label="Postal code" class="w-1/2">
                                                <a-input value="Vietnam" />
                                            </a-form-item>
                                        </div>
                                        <a-form-item label="Phone">
                                            <a-input
                                                v-decorator="[
                                                    'phone',
                                                    { rules: [
                                                        { required: true, message: 'Please input your phone number!' },
                                                        {pattern:/^0\d{9}$/,
                                                         message:'Phone number is in wrong format'}
                                                    ] },
                                                ]"
                                            />
                                            <span>We'll use this if we need to contect you.</span>
                                        </a-form-item>
                                        <a-form-item>
                                            <div class="w-full flex justify-end gap-3 mt-4">
                                                <!-- <button
                                        class="rounded-md border-prim-10 border shadow px-2 py-1
                             bg-gray-100 text-white"
                                        html-type="submit"
                                    >
                                        Pay
                                    </button> -->
                                                <a-button
                                                    style="color: white; background-color: rgb(59, 63, 63);
                             border: none;"
                                                    type="primary"
                                                    html-type="submit"
                                                >
                                                    Pay
                                                </a-button>
                                            </div>
                                        </a-form-item>
                                    </a-form>
                                </div>
                            </div>
                            <div class="w-full bg-white rounded-md border-prim-10 border shadow mt-4">
                                <span :class="[valuePayment === 2 ?'bg-prim-10':'','flex items-center gap-2 p-4 rounded-t-md']">
                                    <a-radio :value="2" />
                                    <font-awesome-icon icon="paypal" style="color: #22deec;" />
                                    <span>
                                        <strong class="text-[#07209F]"><i>Pay</i></strong><strong class="text-[#2EA1FF]"><i>Pal</i></strong>
                                    </span>
                                </span>
                                <div v-if="valuePayment === 2" class="m-4">
                                    <span>Connect your PayPal account and use it to pay your bills. You'll be
                                        redirected to PayPal to add your billing information.</span>
                                    <div class="w-full flex justify-end gap-3 mt-4">
                                        <!-- <button class="rounded-sm border shadow px-8 py-1 flex justify-center items-center">
                                Pay with&nbsp;<strong class="text-[#07209F]"><i>Pay</i></strong><strong class="text-[#2EA1FF]"><i>Pal</i></strong>
                            </button> -->
                                        <a-button block style="max-width: 40%;">
                                            Pay with<strong class="text-[#07209F]"><i>&nbsp;Pay</i></strong><strong class="text-[#2EA1FF]"><i>Pal</i></strong>
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
                        <strong>Basic Shopify plan</strong>
                        <span class="cursor-pointer text-[#4185de]">Change plan</span>
                    </div>
                    <p class=" px-4">
                        You can change or cancel your plan at any time. Prices excl. additional taxes
                    </p>
                    <div class="flex justify-between items-center  p-4 pt-0">
                        <div class="flex gap-2">
                            <a-checkbox indeterminate />
                            <div class="">
                                <strong>Today</strong> <br>
                                <span>Ongoing plan</span>
                            </div>
                        </div>
                        <div class="text-right">
                            <strong>$25.00</strong> <br>
                            <span>billed every 30 day</span>
                        </div>
                    </div>
                    <div class="border-y border-prim-10 flex justify-between p-4 items-center">
                        <strong>Plan details</strong>
                        <a-icon type="up" />
                    </div>
                    <div class="bg-prim-5 p-4 border-y border-prim-10 ">
                        <ul style="list-style: inside;">
                            <li><strong>2 staff members</strong></li>
                            <li>Up to <strong>1,000 locations</strong></li>
                            <li>Shipping discounts</li>
                            <li>Shopify POS for markets and events</li>
                        </ul>
                    </div>
                    <div class="p-4">
                        <div class="flex justify-between mb-4">
                            <strong>Total</strong>
                            <strong>$25.00 USD + tax</strong>
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
                form: this.$form.createForm(this, { name: 'payment' }),
                formBusiness: this.$form.createForm(this, { name: 'Business' }),
            };
        },
        methods: {
            handleSubmitPayment(e) {
                e.preventDefault();
                this.form.validateFields((err, values) => {
                    if (!err) {
                        console.log('Received values of form: ', values);
                    }
                });
            },
            handleSubmitBusiness(e) {
                e.preventDefault();
                this.formBusiness.validateFields((err, values) => {
                    if (!err) {
                        console.log('Received values of form: ', values);
                    }
                });
            },
        },
    };
</script>

<style lang="scss">

</style>

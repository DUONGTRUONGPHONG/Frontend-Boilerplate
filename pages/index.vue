<template>
    <div class="px-8 py-4 bg-prim-5">
        <div class="bg-white rounded-md mb-5">
            <div class="flex flex-col lg:flex-row lg:justify-between lg:items-center p-4 ">
                <div>
                    <span class="font-semibold text-xl">Login activity</span>
                    <p>
                        Check when and where you've logged in to your account.
                    </p>
                </div>
                <button class="text-[#2e8cff] border-[#2ea1ff9c] border py-1 px-3 rounded-lg font-semibold w-fit">
                    Log Out from All Devices
                </button>
            </div>
            <a-table :columns="columns" :data-source="data" :pagination="false" :scroll="{ x: 1000 }">
                <span slot="device" slot-scope="text" class="flex items-center gap-2"><a-icon type="desktop" /><strong>{{ text }}</strong></span>
                <span slot="date" slot-scope="date"><strong>{{ date }}</strong></span>
            </a-table>
            <div class="p-4">
                <a href="#">View Login History</a>
            </div>
        </div>
        <div class="bg-white rounded-md mb-5">
            <div class="p-4 flex items-center gap-2">
                <span class="font-semibold text-xl">Partner dashboard</span><a-icon type="info-circle" style="color:#2e8cff ;" />
            </div>
            <a-divider class="!m-0"/>
            <div class="flex flex-col lg:flex-row lg:justify-between lg:items-center p-4 gap-10">
                <div>
                    Partners are freelancers and agencies that build sites for clients. <br>
                    You can enable or disable the Partner Dashboard here.
                </div>
                <button class="text-[#2e8cff] border-[#2ea1ff9c] border py-1 px-3 rounded-lg font-semibold w-fit">
                    Enable
                </button>
            </div>
        </div>
        <div class="bg-white rounded-md mb-5">
            <div class="p-4">
                <span class="font-semibold text-xl">Privacy preferences</span>
            </div>
            <a-divider class="!m-0"/>
            <div class="flex flex-col lg:flex-row lg:justify-between lg:items-center p-4 gap-10">
                <div>
                    View and manage cookie and privacy preferences for your account. <a href="#">Read More</a>
                </div>
                <button class="text-[#2e8cff] border-[#2ea1ff9c] border py-1 px-3 rounded-lg font-semibold w-fit">
                    Manage Preferences
                </button>
            </div>
        </div>
        <div class="bg-white rounded-md">
            <div class="p-4 flex items-center gap-2">
                <span class="font-semibold text-xl">Close your account</span>
            </div>
            <a-divider class="!m-0"/>
            <div class="flex flex-col lg:flex-row lg:justify-between lg:items-center p-4 gap-10">
                <div>
                    To close your account,first move any remaining sites to Trash.If your site has any Premium Plans <br>
                    or domains connected, you'll need to cancel or transfer them first. <a href="#">Learn More</a>
                </div>
                <button class="text-[#E82727] border-[#e84a2742] border py-1 px-3 rounded-lg font-semibold w-fit ">
                    Close your account
                </button>
            </div>
        </div>
    </div>
</template>

<script>
    const columns = [
        {
            title: 'Device',
            dataIndex: 'device',
            key: 'device',
            scopedSlots: { customRender: 'device' },
        },
        {
            title: 'Location',
            dataIndex: 'location',
            key: 'location',
            // width: 80,
        },
        {
            title: 'Date',
            dataIndex: 'date',
            key: 'date',
            scopedSlots: { customRender: 'date' },
        },
        {
            title: 'Browser',
            dataIndex: 'browser',
            key: 'browser',
            // ellipsis: true,
        },
    ];

    const data = [
        {
            key: '1',
            device: 'Windows',
            location: 'Hanoi,Vietnam',
            date: 'Current Session',
            browser: 'Chrome',
        },
    ];
    export default {
        auth: false,
        data() {
            return {
                data,
                columns,
            };
        },
        head() {
            return {
                title: 'Dashboard | Nuxt Boilerplate',
            };
        },
    };
</script>

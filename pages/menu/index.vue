<template>
    <div class="flex justify-center">
        <a-popover placement="bottomRight" trigger="click">
            <template slot="content">
                <div class="flex gap-3 items-center border-info-40 border-b py-3 px-4 ">
                    <a-avatar :size="40" icon="user" class="!flex !justify-center !items-center " />
                    <div class="info ">
                        <h5 class="font-extrabold hover:text-prim-100 cursor-pointer">
                            Albert Flores
                        </h5>
                        <p>flodes@doe.io</p>
                    </div>
                </div>
                <div class="!border-b-0 py-3 px-4 cursor-pointer hover:text-prim-100">
                    <p>My Profile</p>
                </div>
                <div class="!border-b-0 pb-3 px-4 cursor-pointer hover:text-prim-100">
                    <p>Account Settings</p>
                </div>
                <div class="!border-info-40 pb-3 px-4 cursor-pointer hover:text-prim-100">
                    <p>Activity Log</p>
                </div>
                <div class="py-3 px-4 cursor-pointer hover:text-prim-100 border-info-40 border-t">
                    <p class="m-0">
                        Sign Out
                    </p>
                </div>
            </template>
            <a-avatar :size="50" icon="user" class="!flex !justify-center !items-center cursor-pointer" />
        </a-popover>
    </div>
</template>

<script>
    export default {
        auth: false,
    };
</script>
<style>
.ant-popover-inner{
    @apply  rounded-md border-info-40 border
}
.ant-popover-arrow{
    @apply !border-info-40 border !border-b-transparent !border-r-transparent z-10 bg-white
}
.ant-popover-inner-content{
    @apply p-0 min-w-[250px]
}
.info h5,p,span{
    @apply m-0 font-semibold
}
.ant-popover-placement-bottomRight > .ant-popover-content > .ant-popover-arrow{
    right: 23px;
}
</style>

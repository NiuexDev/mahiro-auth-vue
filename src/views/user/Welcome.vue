<template>
    <div class="container">
        <!-- <div> -->
        <n-tabs class="box" animated :value="step">
            <n-tab-pane :name="1" display-directive="show">
                <h1>欢迎使用{{ "〇Auth" }}！</h1>
                <div class="info" style="margin: 32px 0;">
                    <p>在使用之前，让我们来进行一些初始化设置。你也可以先跳过，之后再设置。</p>
                    <p>这大约需要2分钟时间。让我们开始吧。</p>
                </div>
                <n-flex class="button" :size="12" justify="end">
                    <n-button tertiary round @click="skip()">跳过</n-button>
                    <n-button type="primary" secondary round @click="nextStep()">下一步</n-button>
                </n-flex>
            </n-tab-pane>

            <n-tab-pane :name="2" display-directive="show">
                <h1>名称</h1>
                <div class="info">
                    <p>设置你在MC中的ID</p>
                    <p>应为4~6字符，只包含字母、数字以及下划线。</p>
                </div>
                <n-form-item :show-label="false">
                    <n-input v-model:value="id" placeholder=""/>
                </n-form-item>
                <n-flex class="button" :size="12" justify="space-between" style="margin-top: 0;">
                    <n-button tertiary round @click="prevStep()">上一步</n-button>
                    <n-button type="primary" secondary round @click="nextStep()">下一步</n-button>
                </n-flex>
            </n-tab-pane>

            <n-tab-pane :name="3" display-directive="show">
                <h1>皮肤</h1>
                <div class="info">
                    <p>设置你在MC中的皮肤</p>
                    <p>需要是64×64的png格式。</p>
                </div>
                <n-upload
                    accept="image/png"
                    :show-file-list="false">
                    <n-upload-dragger>
                        <div style="margin-bottom: 12px">
                            <n-icon size="3em" :depth="5">
                                <UploadRound/>
                            </n-icon>
                        </div>
                        点击或者拖动文件到该区域来上传
                    </n-upload-dragger>
                </n-upload>
                <n-flex class="button" :size="12" justify="space-between">
                    <n-button tertiary round @click="prevStep()">上一步</n-button>
                    <n-button type="primary" secondary round @click="nextStep()">下一步</n-button>
                </n-flex>
            </n-tab-pane>
        </n-tabs>

        <!-- </div> -->
        <div class="bg"></div>
    </div>
</template>

<script lang="ts" setup>
import { ref } from "vue"
import { NTabPane, NTabs, NFlex, NButton, NInput, NFormItem, NUpload, NUploadDragger, NIcon, NText } from "naive-ui"
import { UploadRound } from "@vicons/material"
import { useRouter } from "vue-router"

const router = useRouter()

const step = ref(1)

const id = ref("")

const skip = () => {
    router.replace("/user")
}

const prevStep = () => {
    step.value = step.value <= 0? step.value = 0: step.value-1
}

const nextStep = () => {
    step.value++
}
</script>

<style scoped>
.container {
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
}

.bg {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: url(@a/img/Girls_Band_Cry_KV2.webp);
    background-position: center;
    background-repeat: repeat-x;
    background-size: contain;
    z-index: -1;
}

.box {
    width: min(340px, 100%);
    overflow: hidden;
    box-sizing: border-box;
    padding: 40px;
    box-shadow: 0 0 20px -5px rgba(0, 0, 0, 0.05);
    border-radius: 20px;
    transition: box-shadow 200ms ease
}

@supports (backdrop-filter: blur(10px)) {
    .box {
        background-color: rgba(255, 255, 255, 0.9);
        backdrop-filter: blur(10px);
    }
}

@supports not (backdrop-filter: blur(10px)) {
    .box {
        background-color: #fff;
    }
}


.box:hover {
    box-shadow: 0 0 20px -5px rgba(0, 0, 0, 0.1);
}

.box :deep(h1) {
    margin-bottom: 18px;
}

.box :deep(p) {
    line-height: 1.8em;
    margin: 0.5em 0;
}

.box :deep(.n-tabs-pane-wrapper) {
    overflow: visible;
}

.box :deep(.n-tabs-nav-scroll-wrapper) {
    display: none !important;
}

.box :deep(.n-tab-pane) {
    padding: 0 !important;
}

.info {
    margin: 12px 0;
}

.button {
    margin-top: 14px;
}
</style>
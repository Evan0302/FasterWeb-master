<template>
    <el-dialog title="导入Excel文件"
               :visible.sync="visible"
               center
               @close="$emit('update:ishow', false)"
               :show="ishow"
    >
        <el-upload class="upload-excel"
                   ref="upload"
                   :action="uploadExcel()"
                   :limit="1"
                   :on-preview="handlePreview"
                   :on-remove="handleRemove"
                   :on-success="uploadSuccess"
                   :data="getformdata()"
                   :on-change="fileChange"
                   :file-list="fileList"
                   :auto-upload="false"
                   :headers="headersetting"
                    >
            <el-button slot="trigger" size="small" type="primary">选取文件</el-button>
            <el-button style="margin-left: 10px;" size="small" type="success" @click="submitUpload">上传到服务器</el-button>
            <div slot="tip" class="el-upload__tip">只能上传Excel文件，且不超过500kb</div>
            <!--            <span>{{ this.node}}, {{ this.project }}</span>-->


        </el-upload>
        <el-select v-model="sheetname" placeholder="请选择导入的sheet" v-show="sheetCanSelect">
            <el-option
                v-for="item in sheets"
                :key="item"
                :value="item">
            </el-option>
        </el-select>
<!--        <upload-excel-component :on-success="handleSuccess" :before-upload="beforeUpload"/>-->
        <!--        <span color="#409EFF"> &#45;&#45; </span><br/>-->
        <!--        <el-button @click="visible = false" size="small">取 消</el-button>-->
        <!--        <el-button type="primary" @click="submitUpload" size="small">确 定</el-button>-->

    </el-dialog>
</template>
<script>
    // import UploadExcelComponent from './UploadExcel'
    // import XLSX from "xlsx";
    import store from "../../../../store/state";

    export default {
        name: "upxlsDialog",
        // components: {UploadExcelComponent},
        props: {
            ishow: {
                type: Boolean,
                default: false
            },
            node: {
                require: true
            },
            project: {
                require: true
            },
        },
        data() {
            return {
                loading: false,
                fileList: [],
                visible: this.ishow,
                sheetname: '',
                sheets: {},
                sheetCanSelect: false,
                headersetting:{Authorization :`JWT ${store.token}`},
            };
        },
        watch: {
            ishow(val) {
                this.visible = this.ishow;
                if (!this.ishow) this.resetSelect();
            }
        },
        methods: {

            uploadExcel() {
                return this.$api.excelImport();
            },
            uploadSuccess(response, file, fileList) {
                this.resetSelect();
                this.visible = false;
                this.fileList = [];
            },
            submitUpload() {
                this.$refs.upload.submit();
            },
            handleRemove(file, fileList) {
                this.fileChange(file, fileList);
                console.log(file, fileList);
            },
            handlePreview(file) {
                console.log(file);
            },
            resetSelect(){
                this.sheetCanSelect=false;
                this.sheets={};
                this.sheetname=''
            },
            fileChange(file, fileList) {
                if (fileList.length>0) {
                    this.readerData(file.raw)
                    // this.$message({
                    //     message: '要打开的文件在这里.' + JSON.stringify(this.sheets),
                    //     type: 'info'
                    // })
                    this.sheetCanSelect=true
                }else{
                    this.resetSelect()
                }
            },
            getformdata() {
                return {
                    "nodeid": this.node,
                    "projectid": this.project,
                    "sheetname": this.sheetname
                }
            },
            readerData(rawFile) {
                this.loading = true
                return new Promise((resolve, reject) => {
                    const reader = new FileReader()
                    reader.onload = e => {
                        const data = e.target.result
                        const workbook = XLSX.read(data, {type: 'array'})

                        workbook.SheetNames.map((item,index,ary ) => {
                            // console.log(item)
                            this.sheets[item]=item
                        })
                        this.sheetname = workbook.SheetNames[0]
                        this.loading = false
                        resolve()
                    }
                    reader.readAsArrayBuffer(rawFile)
                })
            },
            beforeUpload(file) {
                const isLt1M = file.size / 1024 / 1024 < 1

                if (isLt1M) {
                    return true
                }

                this.$message({
                    message: 'Please do not upload files larger than 1m in size.',
                    type: 'warning'
                })
                return false
            },
            handleSuccess({results, header}) {
                this.$message({
                    message: '要打开的文件在这里.' + JSON.stringify(results),
                    type: 'info'
                })
            }
        }
    }
</script>


<style scoped>

</style>

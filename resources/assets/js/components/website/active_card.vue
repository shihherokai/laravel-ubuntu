<template>
	<div>
		<el-breadcrumb separator-class="el-icon-arrow-right">
			<el-breadcrumb-item :to="{ path: '/' }">首頁</el-breadcrumb-item>
			<el-breadcrumb-item>網站管理</el-breadcrumb-item>
			<el-breadcrumb-item>活動卡片</el-breadcrumb-item>
		</el-breadcrumb>
	    <el-row type="flex" align="middle">
	    	<el-col :xs="{span: 20, offset: 0}" :sm="{span: 20, offset: 0}">
				<div class="title--orange">活動卡片</div>
	    	</el-col>
	    	<el-col class="u-text-right">
				<el-button type="primary" @click="createFormVisible = true">新增資料</el-button>
	    	</el-col>
	    </el-row>
		<el-table
			:data="tableData"
			style="width: 100%"
			class="u-text-center">
			<el-table-column
				prop="title"
				label="標題">
			</el-table-column>
			<el-table-column
				prop="content"
				label="內容">
			</el-table-column>
			<el-table-column
				fixed="right"
				label="操作">
				<template slot-scope="scope">
					<el-button type="text" size="small" @click="edit(scope.row.id, scope.row.title, scope.row.image, scope.row.content, scope.row.url1, scope.row.url2, scope.row.date_start, scope.row.date_end, scope.row.status)">編輯</el-button>
					<el-button type="text" size="small" @click="del(scope.row.id)">刪除</el-button>
				</template>
			</el-table-column>
		</el-table>

		<!-- 新增資料視窗 -->
		<el-dialog title="新增資料" :visible.sync="createFormVisible" center >
			<el-form ref="createDate" label-width="80px">
				<el-form-item label="標題">
					<el-input v-model="createDate.title"></el-input>
				</el-form-item>
				<el-form-item label="圖片網址">
					<el-input v-model="createDate.image"></el-input>
				</el-form-item>
				<el-form-item label="內容">
					<el-input type="textarea" v-model="createDate.content"></el-input>
				</el-form-item>
				<el-form-item label="連結1">
					<el-input v-model="createDate.url1"></el-input>
				</el-form-item>
				<el-form-item label="連結2">
					<el-input v-model="createDate.url2"></el-input>
				</el-form-item>
				<el-form-item label="開始時間">
					<el-date-picker type="date" placeholder="選擇日期" v-model="createDate.date_start" style="width: 100%;"></el-date-picker>
				</el-form-item>
				<el-form-item label="結束時間">
					<el-date-picker type="date" placeholder="選擇日期" v-model="createDate.date_end" style="width: 100%;"></el-date-picker>
				</el-form-item>
				<el-form-item label="公開">
					<el-switch v-model="createDate.status"></el-switch>
				</el-form-item>
				<div class="u-text-right">
					<el-button @click="createFormVisible = false">取 消</el-button>
					<el-button type="primary" @click="createFormVisible = false">確 定</el-button>
				</div>
			</el-form>
		</el-dialog>

		<!-- 編輯資料視窗 -->
		<el-dialog title="編輯資料" :visible.sync="editFormVisible" center>
			<el-form ref="editData" :model="editData" label-width="80px">
				<el-form-item label="標題">
					<el-input v-model="editData.title"></el-input>
				</el-form-item>
				<el-form-item label="圖片網址">
					<el-input v-model="editData.image"></el-input>
				</el-form-item>
				<el-form-item label="內容">
					<el-input type="textarea" v-model="editData.content"></el-input>
				</el-form-item>
				<el-form-item label="連結1">
					<el-input v-model="editData.url1"></el-input>
				</el-form-item>
				<el-form-item label="連結2">
					<el-input v-model="editData.url2"></el-input>
				</el-form-item>
				<el-form-item label="開始時間">
					<el-date-picker type="date" placeholder="選擇日期" v-model="editData.date_start" style="width: 100%;"></el-date-picker>
				</el-form-item>
				<el-form-item label="結束時間">
					<el-date-picker type="date" placeholder="選擇日期" v-model="editData.date_end" style="width: 100%;"></el-date-picker>
				</el-form-item>
				<el-form-item label="公開">
					<el-switch v-model="editData.status"></el-switch>
				</el-form-item>
				<div class="u-text-right">
					<el-button @click="editFormVisible = false">取 消</el-button>
					<el-button type="primary" @click="editFormVisible = false">儲 存</el-button>
				</div>
			</el-form>
		</el-dialog>
    </div>
</template>

<script>
export default {
    data() {
		return {
        	createFormVisible: false,
        	createDate:{
        		title: '',
        		image: '',
        		content: '',
        		url1: '',
        		url2: '',
        		date_start: '',
        		date_end: '',
        		status:''
        	},
        	editFormVisible: false,
        	editData:{
        		id: '',
        		title: '',
        		image: '',
        		content: '',
        		url1: '',
        		url2: '',
        		date_start:  '',
        		date_end:  '',
        		status: ''
        	},
			tableData: [{
				id:'1',
        		title:'測試A',
        		image: 'https://firebasestorage.googleapis.com/v0/b/tripmatchwebsite.appspot.com/o/img%2Ftrip05%20(1).png?alt=media&token=731a240e-df1d-4bf7-8b69-23f43c21fe03',
				content:'測試文字ABCDEFGHIJKLMNOPQRSTUVWXYZ',
        		url1:'https://url1',
        		url2:'https://url2',
        		date_start:'2017-01-01',
        		date_end:'2017-12-02',
        		status:true,
			}, {
				id:'2',
        		title:'測試B',
        		image: 'https://firebasestorage.googleapis.com/v0/b/tripmatchwebsite.appspot.com/o/img%2Ftrip05%20(1).png?alt=media&token=731a240e-df1d-4bf7-8b69-23f43c21fe03',
				content:'測試文字ABCDEFGHIJKLMNOPQRSTUVWXYZ',
        		url1:'https://url1',
        		url2:'https://url2',
        		date_start:'2017-01-01',
        		date_end:'2017-05-02',
        		status:true,
			}, {
				id:'3',
        		title:'測試C',
        		image: 'https://firebasestorage.googleapis.com/v0/b/tripmatchwebsite.appspot.com/o/img%2Ftrip05%20(1).png?alt=media&token=731a240e-df1d-4bf7-8b69-23f43c21fe03',
				content:'測試文字ABCDEFGHIJKLMNOPQRSTUVWXYZ',
        		url1:'https://url1',
        		url2:'https://url2',
        		date_start:'2017-01-01',
        		date_end:'2017-01-02',
        		status:false,
			}, {
				id:'4',
        		title:'測試D',
        		image: 'https://firebasestorage.googleapis.com/v0/b/tripmatchwebsite.appspot.com/o/img%2Ftrip05%20(1).png?alt=media&token=731a240e-df1d-4bf7-8b69-23f43c21fe03',
				content:'測試文字ABCDEFGHIJKLMNOPQRSTUVWXYZ',
        		url1:'https://url1',
        		url2:'https://url2',
        		date_start:'2017-01-01',
        		date_end:'2017-01-02',
        		status:true,
			}]
		}
	},
	methods: {
		edit(id, title, image, content, url1, url2, date_start, date_end, status){
			this.editData.id = id;
			this.editData.title = title;
			this.editData.image = image;
			this.editData.content = content;
			this.editData.url1 = url1;
			this.editData.url2 = url2;
			this.editData.date_start = date_start;
			this.editData.date_end = date_end;
			this.editData.status = status;
			this.editFormVisible = true;
		},
		del(id){
			this.$confirm('此操作將刪除該筆資料，確定嗎?', '提示', {
				confirmButtonText: '確定',
				cancelButtonText: '取消',
				type: 'warning'
			}).then(() => {
				this.$message({
					type: 'success',
					message: '刪除成功'
				});
				console.log('刪除成功的操作');
			}).catch(() => {
				this.$message({
					type: 'info',
					message: '已取消操作'
				});
				console.log('刪除取消的操作');
			});
		},
	}
}
</script>
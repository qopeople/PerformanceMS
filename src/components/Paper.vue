<template>
<form name="paperForm" method="post" action="/business/paper/paper.do" enctype="multipart/form-data">
<input type="hidden" name="actionType" value="add">
<input type="hidden" name="pageType" value="add">
<input type="hidden" name="bean.id" value="">
<input type="hidden" name="strselected" value="">
<input type="hidden" name="sameNameSave" value="">
<input type="hidden" name="bean.firstAuthorId" value="5b5e3f773b17f461013b1be976520c21">
<input type="hidden" name="bean.txzzId" value="">
<input type="hidden" name="bean.paperSource" value="录入">
<input type="hidden" name="projectIndex"/>
<input type="hidden" name="reshipIndex"/>
<input type="hidden" name="existSameRecord" value="false">
<el-card class="box-card">
<div slot="header" class="clearfix">
    <span style="font-weight:bold;">论文新增</span>
    <el-button style="float: right; padding: 3px 0" type="text">操作按钮</el-button>
  </div>
<el-tabs type="border-card">
	<el-tab-pane label="基本信息">
		  <table id="table" cellspacing="0" cellpadding="0" align="center">
	<div>
		<tr>
			<td class='tdrowhead' colspan=1 rowspan=1 width='15%'>论文类型：</td>
			<td class='list' colspan=3 rowspan=1><div id='paper.paperModeId'>	
			<el-radio v-model="P_paperModeId" name='bean.paperModeId' label="1" value='1' >期刊论文</el-radio>
			<el-radio v-model="P_paperModeId" name='bean.paperModeId' label="2" value='2' >论文集</el-radio>
			<el-radio v-model="P_paperModeId" name='bean.paperModeId' label="3" value='3' >文章</el-radio>
		<font color=red> *</font></div></td>
		</tr>
		<tr>
			<td class='tdrowhead' colspan=1 rowspan=1 width='15%'>论文题目：</td>
			<td class='list' colspan=3 rowspan=1><div id='paper.name'> 
			<el-input type='text' name='bean.name'  id='name' size=70   maxLength = '512' ></el-input ><font color=red> *</font></div></td>
		</tr>
		<tr>
			<td class='tdrowhead' colspan=1 rowspan=1 width='15%'>学科门类：</td>
			<td class='list' colspan=1 rowspan=1 width='35%'><div id='paper.subjectClassId'>	
			<el-radio v-model="P_subjectClassId" name='bean.subjectClassId' label="1" value='1'>科技类</el-radio>
			<el-radio v-model="P_subjectClassId" name='bean.subjectClassId' label="2" value='2'>社科类</el-radio>
            <font color=red> *</font></div></td>
			<td class='tdrowhead' colspan=1 rowspan=1 width='15%'>发表/出版时间：</td>
			<td class='list' colspan=1 rowspan=1 width='35%'><div id='paper.publishDate'> 
			<el-date-picker type='date' name='bean.publishDate'  id='publishDate' size=12 v-model="P_publishDate"  placeholder="选择日期" suffix-icon="el-icon-date"  class="Wdate" ></el-date-picker>
			<font color=red> *</font></div></td>
		</tr>
		<tr>
			<td class='tdrowhead' colspan=1 rowspan=1 width='15%' title='“刊物级别”提供文字检索功能。例如：输入拼音“管理评论”即可显示期刊“管理评论”'>发表刊物/论文集：</td>
			<td class='list' colspan=3 rowspan=1 title='“刊物级别”提供文字检索功能。例如：输入拼音“管理评论”即可显示期刊“管理评论”'><div id='paper.publishUnit'> 
			<el-input type='text' name='bean.publishUnit'  id='publishUnit' size=30 value=""   maxLength = '128' ></el-input ><font color=red> *</font></div></td>
		</tr>
		<tr>
			<td class='tdrowhead' colspan='1' rowspan='1' width='15%'>刊物类型：</td>
			<td  colspan='3' rowspan='1' >
			<el-checkbox-group v-model="P_paperTypes">
				<el-checkbox label="CSSCI扩展版"></el-checkbox>
				<el-checkbox label="CSSCI来源刊"></el-checkbox>
				<el-checkbox label="CSSCI收录集刊"></el-checkbox>
				<el-checkbox label="CSSCI"></el-checkbox>
				<el-checkbox label="SCI"></el-checkbox>
				<el-checkbox label="EI"></el-checkbox>
				<el-checkbox label="ISTP"></el-checkbox><br>
				<el-checkbox label="核心期刊"></el-checkbox>
				<el-checkbox label="一般期刊"></el-checkbox>
				<el-checkbox label="人大复印转载"></el-checkbox>	
				<el-checkbox label="T类一级期刊"></el-checkbox>
				<el-checkbox label="T类二级期刊"></el-checkbox>
				<el-checkbox label="T类三级期刊"></el-checkbox><br>
				<el-checkbox label="A类重要期刊"></el-checkbox>
				<el-checkbox label="B类重要期刊"></el-checkbox>
				<el-checkbox label="C类重要期刊"></el-checkbox>
				<el-checkbox label="D类重要期刊"></el-checkbox>
				<el-checkbox label="东莞理工学院学报"></el-checkbox>
			</el-checkbox-group>
			</td>
		</tr>
		<br>
		<tr class="employType">
			<td class='tdrowhead' colspan='1' rowspan='1' width='15%' >收录类别：</td>
			<td  colspan='3' rowspan='1' >
				<el-checkbox-group v-model="P_employType">
					<el-checkbox label="《中国社会科学文摘》"></el-checkbox>
					<el-checkbox label="《新华文摘》"></el-checkbox>
					<el-checkbox label="人文社科A类重要期刊"></el-checkbox>
					<el-checkbox label="来源刊"></el-checkbox><br>
					<el-checkbox label="CSSCI"></el-checkbox>
					<el-checkbox label="SSCI"></el-checkbox>
					<el-checkbox label="A&HCI"></el-checkbox>
				</el-checkbox-group>
			</td >
		</tr>
		<tr>
		<td class='tdrowhead' colspan=1 rowspan=1 width='15%'>所属单位：</td>
		<td class='list' colspan=1 rowspan=1 width='35%'><div id='paper.unitId'>
			<el-select v-model="P_unitId"  name='bean.unitId' placeholder="请选择">
				<el-option
				v-for="item in P_unitIds"
				:key="item.value"
				:label="item.label"
				:value="item.value">
				</el-option>
			</el-select>
			<font color=red> *</font></div></td>
			<td class='tdrowhead' colspan=1 rowspan=1 width='15%'>一级学科：</td>
			<td class='list' colspan=1 rowspan=1 width='35%'><div id='paper.subjectId'>
			<el-select v-model="P_subjectId"  name='bean.subjectId' placeholder="请选择">
				<el-option
				v-for="item in P_subjectIds"
				:key="item.value"
				:label="item.label"
				:value="item.value">
				</el-option>
			</el-select>
			<font color=red> *</font></div></td>
		</tr>
		<tr>
			<td class='tdrowhead' colspan=1 rowspan=1 width='15%'>项目来源：</td>
			<td class='list' colspan=1 rowspan=1 width='35%'><div id='paper.projectSourceId'>
				<el-select v-model="P_projectSourceId"  name='bean.projectSourceId' placeholder="请选择">
					<el-option
					v-for="item in P_projectSourceIds"
					:key="item.value"
					:label="item.label"
					:value="item.value">
					</el-option>
				</el-select>
				<font color=red> *</font></div>
			</td>
				<td class='tdrowhead' colspan=1 rowspan=1 width='15%'>研究类别：</td>
				<td class='list' colspan=1 rowspan=1 width='35%'><div id='paper.researchClassId'>
				<el-select v-model="P_researchClassId"  name='bean.researchClassId' placeholder="请选择">
					<el-option value='' >--请选择--</el-option>
					<el-option value='基础研究' >基础研究</el-option>
					<el-option value='实验与发展' >实验与发展</el-option>
					<el-option value='应用研究' >应用研究</el-option>
				</el-select>
				<font color=red> *</font></div></td>
		</tr>
		<tr>
			<td class='tdrowhead' colspan=1 rowspan=1 width='15%'>发表范围：</td>
			<td class='list' colspan=1 rowspan=1 width='35%'><div id='paper.publishRangeId'>
					<el-select v-model="P_publishRangeId"  name='bean.publishRangeId' placeholder="请选择">
						<el-option value='' >--请选择--</el-option>
						<el-option value='国外学术期刊' >国外学术期刊</el-option>
						<el-option value='国内外公开发行' >国内外公开发行</el-option>
						<el-option value='国内公开发行' >国内公开发行</el-option>
						<el-option value='港澳台刊物' >港澳台刊物</el-option>
					</el-select><font color=red> *</font></div></td>
			<td class='tdrowhead' colspan=1 rowspan=1 width='15%'>卷号：</td>
			<td class='list' colspan=1 rowspan=1 width='35%'><div id='paper.juanNumber'> 
				<el-input  v-model="P_juanNumber" name='bean.juanNumber'  id='juanNumber' size=5 maxLength = '32' ></el-input></div></td>
		</tr>
		<tr>
			<td class='tdrowhead' colspan=1 rowspan=1 width='15%'>期号：</td>
			<td class='list' colspan=1 rowspan=1 width='35%'><div id='paper.qiNumber'> <el-input v-model="P_qiNumber" name='bean.qiNumber'  id='qiNumber' size=5   maxLength = '32' ></el-input></div></td>
			<td class='tdrowhead' colspan=1 rowspan=1 width='15%'>页码范围：</td>
			<td class='list' colspan=1 rowspan=1 width='35%'><div id='paper.pageScope'> <el-input v-model="P_pageScope" name='bean.pageScope'  id='pageScope' size=0   maxLength = '128' ></el-input></div></td>
		</tr>
		<tr>
			<td class='tdrowhead' colspan=1 rowspan=1 width='15%'>字数：</td>
			<td class='list' colspan=1 rowspan=1 width='35%'><div id='paper.wordNumber'> <el-input v-model="P_wordNumber" name='bean.wordNumber'  id='wordNumber' size=5 value="0.0"></el-input>&nbsp;万字</div></td>
			<td class='tdrowhead' colspan=1 rowspan=1 width='15%'>学校署名：</td>
			<td class='list' colspan=1 rowspan=1 width='35%'><div id='paper.schoolSign'>	
				<el-radio v-model="P_schoolSign" name='bean.schoolSign' label="0" value='0'  >第一单位</el-radio>
				<el-radio v-model="P_schoolSign" name='bean.schoolSign' label="1" value='1'  >非第一单位</el-radio>

		</div></td>
		</tr>
		<tr>
			<td class='tdrowhead' colspan=1 rowspan=1 width='15%'>单位排名：</td>
			<td class='list' colspan=1 rowspan=1 width='35%'><div id='paper.unitOrderId'>
					<el-select v-model="P_unitOrderId"  name='bean.unitOrderId' placeholder="请选择">
						<el-option value='' >--请选择--</el-option>
						<el-option value='1' >第1</el-option>
						<el-option value='2' >第2</el-option>
						<el-option value='3' >第3</el-option>
						<el-option value='4' >第4</el-option>
						<el-option value='5' >第5</el-option>
						<el-option value='6' >第6</el-option>
						<el-option value='7' >第7</el-option>
						<el-option value='8' >第8</el-option>
						<el-option value='9' >第9</el-option>
						<el-option value='10' >第10</el-option>
					</el-select>单位<font color=red> *</font></div></td>
			<td class='tdrowhead' colspan=1 rowspan=1 width='15%'>版面：</td>
			<td class='list' colspan=1 rowspan=1 width='35%'><div id='paper.pageSpace'>	
				<el-radio v-model="P_pageSpace" name='bean.pageSpace' label="1" value='1'  >正常版面</el-radio>
				<el-radio v-model="P_pageSpace" name='bean.pageSpace' label="2" value='2'  >增刊</el-radio>
				<el-radio v-model="P_pageSpace" name='bean.pageSpace' label="3" value='3'  >年刊</el-radio>
				<el-radio v-model="P_pageSpace" name='bean.pageSpace' label="4" value='4'  >专刊</el-radio>

			</div></td>
		</tr>
		<tr>
			<td class='tdrowhead' colspan=1 rowspan=1 width='15%'>是否为译文：</td>
			<td class='list' colspan=1 rowspan=1 width='35%'><div id='paper.isTranslated'>	
				<el-radio v-model="P_isTranslated" name='bean.isTranslatelabel' label="0" value='0'  >否</el-radio>
				<el-radio v-model="P_isTranslated" name='bean.isTranslatelabel' label="1" value='1'  >是</el-radio>

			</div></td>
			<td class='tdrowhead' colspan=1 rowspan=1 width='15%'>ISSN号：</td>
			<td class='list' colspan=1 rowspan=1 width='35%'><div id='paper.issn'> 
				<el-input v-model="P_issn" name='bean.issn'  id='issn' size=0 maxLength = '100' ></el-input></div></td>
		</tr>
		<tr>
			<td class='tdrowhead' colspan=1 rowspan=1 width='15%'>索引号：</td>
			<td class='list' colspan=1 rowspan=1 width='35%'><div id='paper.referenceNumber'> 
				<el-input v-model="P_referenceNumber" name='bean.referenceNumber'  id='referenceNumber' size=0></el-input></div></td>
			<td class='tdrowhead' colspan=1 rowspan=1 width='15%'>CN号：</td>
			<td class='list' colspan=1 rowspan=1 width='35%'><div id='paper.cn'> 
				<el-input v-model="P_cn" name='bean.cn'  id='cn' size=0 maxLength = '100' ></el-input></div></td>
		</tr>
		<tr>
			<td class='tdrowhead' colspan=1 rowspan=1 width='15%'>是否正式出版：</td>
			<td class='list' colspan=3 rowspan=1><div id='paper.isOfficialPublish'>	
			<el-radio v-model="P_isOfficialPublish" name='bean.isOfficialPublish' label="0" value='0'  >否</el-radio>
			<el-radio v-model="P_isOfficialPublish" name='bean.isOfficialPublish' label="1" value='1'  >是</el-radio>

		<font color=red> *</font></div></td>
		</tr>
	</div>
	</table>
	</el-tab-pane>
	<el-tab-pane label="论文作者">
			<el-table
				:data="tableData"
				stripe
				style="width: 100%">
				<el-table-column prop="P_orderId" label="署名顺序" width="115"></el-table-column>
				<el-table-column prop="P_authorType" label="作者类型" width="115"></el-table-column>
				<el-table-column prop="P_authorName" label="作者姓名" width="115"></el-table-column>
				<el-table-column prop="P_sexId" label="作者职工号" width="115"></el-table-column>
				<el-table-column prop="P_authorCode" label="性别" width="115"></el-table-column>
				<el-table-column prop="P_subject" label="学历" width="115"></el-table-column>
				<el-table-column prop="P_titleId" label="职称" width="115"></el-table-column>
				<el-table-column prop="P_authorUnit" label="是否通讯作者" width="115"></el-table-column>
				<el-table-column prop="P_authorUnit" label="工作单位" width="115"></el-table-column>
				<el-table-column prop="P_workRatio" label="贡献率" width="115"></el-table-column>
			</el-table>
	</el-tab-pane>
</el-tabs>
</el-card>


</form> 
</template>


<script>
  export default {
    data() {  
      return {
        activeIndex:'1',
        activeIndex2:'1',
        P_name:'',
        P_paperModeId:'',
        P_subjectClassId:'',
        P_publishDate:'',
        P_publishUnit:'',
        P_paperTypes:[],
        P_employType:[],
        P_unitId:'',
        P_unitIds:[
			{ value:'',label:'--请选择--'
			},{ value:'教育学院(师范学院)',label:'教育学院(师范学院)'
			},{ value:'经济与管理学院',label:'经济与管理学院'
			},{ value:'生态环境与建筑工程学院',label:'生态环境与建筑工程学院'
			},{ value:'文学与传媒学院',label:'文学与传媒学院'
			},{ value:'城市学院',label:'城市学院'
			},{ value:'电子工程与智能化学院',label:'电子工程与智能化学院'
			},{ value:'法律与社会工作学院（知识产权学院）',label:'法律与社会工作学院（知识产权学院）'
			},{ value:'工程技术研究院',label:'工程技术研究院'
			},{ value:'化学工程与能源技术学院',label:'化学工程与能源技术学院'
			},{ value:'机械工程学院',label:'机械工程学院'
			},{ value:'计算机与网络安全学院',label:'计算机与网络安全学院'
			},{ value:'继续教育学院',label:'继续教育学院'
			},{ value:'科技产业公司',label:'科技产业公司'
			},{ value:'科技创新研究院',label:'科技创新研究院'
			},{ value:'离职人员',label:'离职人员'
			},{ value:'马克思主义学院',label:'马克思主义学院'
			},{ value:'清洁生产科技中心',label:'清洁生产科技中心'
			},{ value:'社会发展研究院',label:'社会发展研究院'
			},{ value:'体育中心（挂靠体育系）',label:'体育中心（挂靠体育系）'
			},{ value:'图书馆',label:'图书馆'
			},{ value:'退休部门',label:'退休部门'
			},{ value:'莞城校区管委会',label:'莞城校区管委会'
			},{ value:'网络空间安全学院',label:'网络空间安全学院'
			},{ value:'网络与教育技术中心',label:'网络与教育技术中心'
			},{ value:'学报',label:'学报'
			},{ value:'学术交流中心',label:'学术交流中心'
			},{ value:'粤台产业科技学院',label:'粤台产业科技学院'
			},{ value:'知识产权中心（挂靠政法学院）',label:'知识产权中心（挂靠政法学院）'
			},{ value:'中法联合学院',label:'中法联合学院'
			},{ value:'组织部',label:'组织部'
			},{ value:'保卫处',label:'保卫处'
			},{ value:'财务处',label:'财务处'
			},{ value:'发展规划处',label:'发展规划处'
			},{ value:'高教研究与评估中心',label:'高教研究与评估中心'
			},{ value:'工会',label:'工会'
			},{ value:'国际交流处',label:'国际交流处'
			},{ value:'后勤集团',label:'后勤集团'
			},{ value:'教师发展中心',label:'教师发展中心'
			},{ value:'教务处',label:'教务处'
			},{ value:'科研处',label:'科研处'
			},{ value:'人事处',label:'人事处'
			},{ value:'人事代理服务处',label:'人事代理服务处'
			},{ value:'审计监察处',label:'审计监察处'
			},{ value:'团委',label:'团委'
			},{ value:'校领导',label:'校领导'
			},{ value:'协同发展创新办公室',label:'协同发展创新办公室'
			},{ value:'宣传部',label:'宣传部'
			},{ value:'学科建设办',label:'学科建设办'
			},{ value:'学生处',label:'学生处'
			},{ value:'学校办公室',label:'学校办公室'
			},{ value:'资产后勤管理处',label:'资产后勤管理处'
			},{ value:'广东高校网络与信息安全工程技术开发中心',label:'广东高校网络与信息安全工程技术开发中心'
			},{ value:'广东高校网络与信息安全工程开发中心',label:'广东高校网络与信息安全工程开发中心'
			},{ value:'广东省科协海智计划东莞理工学院',label:'广东省科协海智计划东莞理工学院'
			},{ value:'广东省社会科学研究基地--东莞理工学院质量与品牌发展研究中心',label:'广东省社会科学研究基地--东莞理工学院质量与品牌发展研究中心'
			},{ value:'广东省无线传感器网络系统及应用工程技术研究中心',label:'广东省无线传感器网络系统及应用工程技术研究中心'
			},{ value:'新时代价值与文化研究中心',label:'新时代价值与文化研究中心'
			},{ value:'生态环境工程技术研发中心',label:'生态环境工程技术研发中心'
		}],
        P_subjectId:'',
        P_subjectIds:[
			{ value:'',label:'--请选择--'
			},{ value:'管理学',label:'管理学'
			},{ value:'马克思主义',label:'马克思主义'
			},{ value:'哲学',label:'哲学'
			},{ value:'宗教学',label:'宗教学'
			},{ value:'语言学',label:'语言学'
			},{ value:'文学',label:'文学'
			},{ value:'艺术学',label:'艺术学'
			},{ value:'历史学',label:'历史学'
			},{ value:'考古学',label:'考古学'
			},{ value:'经济学',label:'经济学'
			},{ value:'政治学',label:'政治学'
			},{ value:'法学',label:'法学'
			},{ value:'军事学',label:'军事学'
			},{ value:'社会学',label:'社会学'
			},{ value:'民族学与文化学',label:'民族学与文化学'
			},{ value:'新闻学与传播学',label:'新闻学与传播学'
			},{ value:'图书馆、情报与文献学',label:'图书馆、情报与文献学'
			},{ value:'教育学',label:'教育学'
			},{ value:'体育科学',label:'文学'
			},{ value:'统计学',label:'统计学'
		}],
        P_projectSourceId:'',
        P_projectSourceIds:[
			{ value:'',label:'--请选择--'
			},{ value:'03',label:'国家社科基金单列学科项目'
			},{ value:'04',label:'国家社科基金项目'
			},{ value:'05',label:'教育部人文社科研究项目'
			},{ value:'051',label:'全国教育科学规划（教育部）项目'
			},{ value:'06',label:'国家自然科学基金项目'
			},{ value:'07',label:'中央其他部门社科专门项目'
			},{ value:'08',label:'高校古籍整理研究项目'
			},{ value:'09',label:'省、市、自治区社科基金项目'
			},{ value:'10',label:'省教育厅社科项目'
			},{ value:'11',label:'地、市、厅、局等政府部门项目'
			},{ value:'12',label:'国际合作研究项目'
			},{ value:'13',label:'与港、澳、台合作研究项目'
			},{ value:'14',label:'企事业单位委托项目'
			},{ value:'15',label:'外资项目'
			},{ value:'16',label:'学校社科项目'
			},{ value:'99',label:'其他研究项目'
			},{ value:'999',label:'无依托项目研究成果'
		}],
        P_researchClassId:'',
        P_publishRangeId:'',
        P_juanNumber:'',
        P_qiNumber:'',
        P_pageScope:'',
        P_wordNumber:'',
        P_schoolSign:'',
        P_unitOrderId:'',
        P_pageSpace:'',
        P_isTranslated:'',
        P_issn:'',
        P_referenceNumber:'',
        P_cn:'',
        P_isOfficialPublish:'',
        P_orderId:'',
        P_authorType:'',
        P_authorTypes:[
			{ value:'',label:'--请选择--'
			},{ value:'1',label:'本校老师'
			},{ value:'2',label:'本校学生'
			},{ value:'3',label:'外校人员'
		}],
        P_authorName:'',
        P_sexId:'',
        P_sexIds:[
		{ value:'',label:'--请选择--'
        },{ value:'1',label:'男'
        },{ value:'2',label:'女'
		}],
        P_authorCode:'',
        P_subject:'',
        P_titleId:'',
        P_titleIds:[
			{ value:'',label:'--请选择--'
			},{ value:'教授',label:'教授'
			},{ value:'团委',label:'团委'
			},{ value:'副教授',label:'副教授'
			},{ value:'助教',label:'助教'
			},{ value:'初级',label:'初级'
			},{ value:'其他人员',label:'其他人员'
			},{ value:'高级讲师',label:'高级讲师'
			},{ value:'讲师',label:'讲师'
			},{ value:'助理讲师',label:'助理讲师'
			},{ value:'教员',label:'教员'
			},{ value:'高级实习指导教师',label:'高级实习指导教师'
			},{ value:'一级实习指导教师',label:'一级实习指导教师'
			},{ value:'二级实习指导教师',label:'二级实习指导教师'
			},{ value:'三级实习指导教师',label:'三级实习指导教师'
			},{ value:'中学高级教师',label:'中学高级教师'
			},{ value:'中学一级教师',label:'中学一级教师'
			},{ value:'中学二级教师',label:'中学二级教师'
			},{ value:'中学三级教师',label:'中学三级教师'
			},{ value:'研究员',label:'研究员'
			},{ value:'副研究员',label:'副研究员'
			},{ value:'助理研究员',label:'助理研究员'
			},{ value:'研究实习员',label:'研究实习员'
			},{ value:'高级实验师',label:'高级实验师'
			},{ value:'实验员',label:'实验员'
			},{ value:'高级工程师',label:'高级工程师'
			},{ value:'工程师',label:'工程师'
			},{ value:'助理工程师',label:'助理工程师'
			},{ value:'技术员',label:'技术员'
			},{ value:'高级经济师',label:'高级经济师'
			},{ value:'经济师',label:'经济师'
			},{ value:'助理经济师',label:'助理经济师'
			},{ value:'经济员',label:'经济员'
			},{ value:'高级会计师',label:'高级会计师'
			},{ value:'会计师',label:'会计师'
			},{ value:'助理会计师',label:'助理会计师'
			},{ value:'会计员',label:'会计员'
			},{ value:'高级统计师',label:'高级统计师'
			},{ value:'统计师',label:'统计师'
			},{ value:'助理统计师',label:'助理统计师'
			},{ value:'统计员',label:'统计员'
			},{ value:'编审',label:'编审'
			},{ value:'副编审',label:'副编审'
			},{ value:'编辑',label:'编辑'
			},{ value:'助理编辑',label:'助理编辑'
			},{ value:'研究馆员',label:'研究馆员'
			},{ value:'副研究馆员',label:'副研究馆员'
			},{ value:'馆员',label:'馆员'
			},{ value:'助理馆员',label:'助理馆员'
			},{ value:'管理员',label:'管理员'
			},{ value:'高级政工师',label:'高级政工师'
			},{ value:'政工师',label:'政工师'
			},{ value:'助理政工师',label:'助理政工师'
			},{ value:'政工员',label:'政工员'
		}],
        P_eduLevelId:'',
        P_eduLevelIds:[
			{ value:'',label:'--请选择--'
			},{ value:'0',label:'博士研究生'
			},{ value:'1',label:'硕士研究生'
			},{ value:'2',label:'本科生'
			},{ value:'3',label:'大专生'
			},{ value:'4',label:'中专生'
			},{ value:'5',label:'其他'
        }],
        P_isTxzz:'',
        P_isTxzz:[
			{ value:'',label:'--请选择--'
			},{ value:'0',label:'否'
			},{ value:'1',label:'是'
        }],
        P_authorUnit:'',
        P_workRatio:'',
        P_keywords:'',
        P_productAbstract:'',
        P_intro:'',
		tableData:[
			{ P_orderId:'1',P_authorType:'本校教师',P_authorName:'王贺',P_sexId:'男',P_authorCode:'2008024',P_subject:'马克思主义',P_titleId:'教师',P_eduLevelId:'博士',P_isTxzz:'否',P_authorUnit:'办公室',P_workRatio:'70%', 
			},{ P_orderId:'1',P_authorType:'本校教师',P_authorName:'王贺',P_sexId:'男',P_authorCode:'2008024',P_subject:'马克思主义',P_titleId:'教师',P_eduLevelId:'博士',P_isTxzz:'否',P_authorUnit:'办公室',P_workRatio:'70%', 
			},{ P_orderId:'1',P_authorType:'本校教师',P_authorName:'王贺',P_sexId:'男',P_authorCode:'2008024',P_subject:'马克思主义',P_titleId:'教师',P_eduLevelId:'博士',P_isTxzz:'否',P_authorUnit:'办公室',P_workRatio:'70%', 
			},{ P_orderId:'1',P_authorType:'本校教师',P_authorName:'王贺',P_sexId:'男',P_authorCode:'2008024',P_subject:'马克思主义',P_titleId:'教师',P_eduLevelId:'博士',P_isTxzz:'否',P_authorUnit:'办公室',P_workRatio:'70%', 
			},{ P_orderId:'1',P_authorType:'本校教师',P_authorName:'王贺',P_sexId:'男',P_authorCode:'2008024',P_subject:'马克思主义',P_titleId:'教师',P_eduLevelId:'博士',P_isTxzz:'否',P_authorUnit:'办公室',P_workRatio:'70%', 
			},{ P_orderId:'1',P_authorType:'本校教师',P_authorName:'王贺',P_sexId:'男',P_authorCode:'2008024',P_subject:'马克思主义',P_titleId:'教师',P_eduLevelId:'博士',P_isTxzz:'否',P_authorUnit:'办公室',P_workRatio:'70%', 
			},{ P_orderId:'1',P_authorType:'本校教师',P_authorName:'王贺',P_sexId:'男',P_authorCode:'2008024',P_subject:'马克思主义',P_titleId:'教师',P_eduLevelId:'博士',P_isTxzz:'否',P_authorUnit:'办公室',P_workRatio:'70%', 
			},{ P_orderId:'1',P_authorType:'本校教师',P_authorName:'王贺',P_sexId:'男',P_authorCode:'2008024',P_subject:'马克思主义',P_titleId:'教师',P_eduLevelId:'博士',P_isTxzz:'否',P_authorUnit:'办公室',P_workRatio:'70%', 
			},{ P_orderId:'1',P_authorType:'本校教师',P_authorName:'王贺',P_sexId:'男',P_authorCode:'2008024',P_subject:'马克思主义',P_titleId:'教师',P_eduLevelId:'博士',P_isTxzz:'否',P_authorUnit:'办公室',P_workRatio:'70%', 
			},{ P_orderId:'1',P_authorType:'本校教师',P_authorName:'王贺',P_sexId:'男',P_authorCode:'2008024',P_subject:'马克思主义',P_titleId:'教师',P_eduLevelId:'博士',P_isTxzz:'否',P_authorUnit:'办公室',P_workRatio:'70%', 
			},{ P_orderId:'1',P_authorType:'本校教师',P_authorName:'王贺',P_sexId:'男',P_authorCode:'2008024',P_subject:'马克思主义',P_titleId:'教师',P_eduLevelId:'博士',P_isTxzz:'否',P_authorUnit:'办公室',P_workRatio:'70%', 
			},{ P_orderId:'1',P_authorType:'本校教师',P_authorName:'王贺',P_sexId:'男',P_authorCode:'2008024',P_subject:'马克思主义',P_titleId:'教师',P_eduLevelId:'博士',P_isTxzz:'否',P_authorUnit:'办公室',P_workRatio:'70%', 
			},{ P_orderId:'1',P_authorType:'本校教师',P_authorName:'王贺',P_sexId:'男',P_authorCode:'2008024',P_subject:'马克思主义',P_titleId:'教师',P_eduLevelId:'博士',P_isTxzz:'否',P_authorUnit:'办公室',P_workRatio:'70%', 
			},{ P_orderId:'1',P_authorType:'本校教师',P_authorName:'王贺',P_sexId:'男',P_authorCode:'2008024',P_subject:'马克思主义',P_titleId:'教师',P_eduLevelId:'博士',P_isTxzz:'否',P_authorUnit:'办公室',P_workRatio:'70%', 
			},{ P_orderId:'1',P_authorType:'本校教师',P_authorName:'王贺',P_sexId:'男',P_authorCode:'2008024',P_subject:'马克思主义',P_titleId:'教师',P_eduLevelId:'博士',P_isTxzz:'否',P_authorUnit:'办公室',P_workRatio:'70%', 
			},{ P_orderId:'1',P_authorType:'本校教师',P_authorName:'王贺',P_sexId:'男',P_authorCode:'2008024',P_subject:'马克思主义',P_titleId:'教师',P_eduLevelId:'博士',P_isTxzz:'否',P_authorUnit:'办公室',P_workRatio:'70%', 
			},{ P_orderId:'1',P_authorType:'本校教师',P_authorName:'王贺',P_sexId:'男',P_authorCode:'2008024',P_subject:'马克思主义',P_titleId:'教师',P_eduLevelId:'博士',P_isTxzz:'否',P_authorUnit:'办公室',P_workRatio:'70%', 
			},{ P_orderId:'1',P_authorType:'本校教师',P_authorName:'王贺',P_sexId:'男',P_authorCode:'2008024',P_subject:'马克思主义',P_titleId:'教师',P_eduLevelId:'博士',P_isTxzz:'否',P_authorUnit:'办公室',P_workRatio:'70%', 
			},{ P_orderId:'1',P_authorType:'本校教师',P_authorName:'王贺',P_sexId:'男',P_authorCode:'2008024',P_subject:'马克思主义',P_titleId:'教师',P_eduLevelId:'博士',P_isTxzz:'否',P_authorUnit:'办公室',P_workRatio:'70%', 
			},{ P_orderId:'1',P_authorType:'本校教师',P_authorName:'王贺',P_sexId:'男',P_authorCode:'2008024',P_subject:'马克思主义',P_titleId:'教师',P_eduLevelId:'博士',P_isTxzz:'否',P_authorUnit:'办公室',P_workRatio:'70%', 
			},{ P_orderId:'1',P_authorType:'本校教师',P_authorName:'王贺',P_sexId:'男',P_authorCode:'2008024',P_subject:'马克思主义',P_titleId:'教师',P_eduLevelId:'博士',P_isTxzz:'否',P_authorUnit:'办公室',P_workRatio:'70%', 
		}],
          }
    },
    methods: {
    }
  }
</script>

<style>
body{
  margin:0 0 0 0;
  font-size: 15px;
}
.el-input{
	width:200px;
}
.employType{
	margin-top: 50px;
}
tr{
	left:100px;
	height:70px;
}
</style>

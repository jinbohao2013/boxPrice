<template>
  <div class="app-container">
    <p style="line-height:35px;">&ensp;报价人员请注意：<br>&ensp;&ensp;&ensp;&ensp;报价：不含装箱费，额外运费（和线下客户运费），税，蛋糕盒底托，深压纹<br>&ensp;双粘盒默认印刷不同，若印刷相同，则需手动减去相应印刷费</p>
    <el-form ref="form" :model="form" label-width="120px">
      <!-- <el-form-item label="盒型类型：" style="margin-bottom: 0;">
        <ul class="imgList">
          <el-popover
            trigger="focus"
            transition="showin">
            <img src="./box-img/07 (1).png" alt="">
            <li slot="reference" :class="[active==1 ? 'activeClass' : '', 'defaultImg']" @click="imgSetActive(1)" ><img src="./box-img/07.png" alt="" srcset=""><span>双插盒</span></li>
          </el-popover>
          <el-popover
            trigger="focus"
            transition="showin">
            <img src="./box-img/06 (1).png" alt="">
            <li slot="reference" :class="[active==2 ? 'activeClass' : '', 'defaultImg']" @click="imgSetActive(2)" ><img src="./box-img/06.png" alt="" srcset=""><span>双插带安全扣盒</span></li>
          </el-popover>
          <el-popover
            trigger="focus"
            transition="showin">
            <img src="./box-img/05 (1).png" alt="">
            <li slot="reference" :class="[active==3 ? 'activeClass' : '', 'defaultImg']" @click="imgSetActive(3)" ><img src="./box-img/05.png" alt="" srcset=""><span>双插带挂钩盒</span></li>
          </el-popover>
          <el-popover
            trigger="focus"
            transition="showin">
            <img src="./box-img/02 (1).png" alt="">
            <li slot="reference" :class="[active==4 ? 'activeClass' : '', 'defaultImg']" @click="imgSetActive(4)" ><img src="./box-img/02.png" alt="" srcset=""><span>扣底盒</span></li>
          </el-popover>
          <el-popover
            trigger="focus"
            transition="showin">
            <img src="./box-img/09 (1).png" alt="">
            <li slot="reference" :class="[active==5 ? 'activeClass' : '', 'defaultImg']" @click="imgSetActive(5)" ><img src="./box-img/09.png" alt="" srcset=""><span>扣底带挂钩盒</span></li>
          </el-popover>
          <el-popover
            trigger="focus"
            transition="showin">
            <img src="./box-img/04 (1).png" alt="">
            <li slot="reference" :class="[active==6 ? 'activeClass' : '', 'defaultImg']" @click="imgSetActive(6)" ><img src="./box-img/04.png" alt="" srcset=""><span>收缩盒</span></li>
          </el-popover>
          <el-popover
            trigger="focus"
            transition="showin">
            <img src="./box-img/01 (1).png" alt="">
            <li slot="reference" :class="[active==7 ? 'activeClass' : '', 'defaultImg']" @click="imgSetActive(7)" ><img src="./box-img/01.png" alt="" srcset=""><span>平口箱盒</span></li>
          </el-popover>
        </ul>
      </el-form-item> -->
      <!-- <el-form-item label="拼版方式：">
        <el-col :span="8">
          <el-select v-model="form.pinbanType" placeholder="请选择拼版方式" @change="pinbanChange();getPrice1()">
            <el-option v-for="item in form.options7" :key="item.value" :label="item.label" :value="item.value">{{ item.label }}</el-option>
          </el-select>
        </el-col>
        <el-col :span="1" style="text-align:center;opacity:0">
          |
        </el-col>
        <el-col :span="8">
          尺寸（mm）：
          <el-input v-model="form.boxl" placeholder="长" size="mini" style="width:60px;padding:0;text-align:center;" @change="pinbanChange();getPrice1()" >f</el-input>
          <span style="display: inline-block;font-size: 20px;">×</span>
          <el-input v-model="form.boxw" placeholder="宽" size="mini" style="width:60px;padding:0;text-align:center;" @change="pinbanChange();getPrice1()">f</el-input>
          <span style="display: inline-block;font-size: 20px;">×</span>
          <el-input v-model="form.boxh" placeholder="高" size="mini" style="width:60px;padding:0;text-align:center;" @change="pinbanChange();getPrice1()">f</el-input>
        </el-col>
      </el-form-item> -->
      <el-form-item label="拼版后的尺寸：">
        <el-col :span="8">
          单位（mm）：
          <el-input v-model="form.boxlenth" placeholder="长" size="mini" style="width:80px;padding:0;text-align:center;" @change="getPrice1()" >f</el-input>
          <span style="display: inline-block;font-size: 20px;">×</span>
          <el-input v-model="form.boxwidth" placeholder="宽" size="mini" style="width:80px;padding:0;text-align:center;" @change="getPrice1()">f</el-input>
        </el-col>
        <el-col :span="1" style="text-align:center;opacity:0">
          |
        </el-col>
        <el-col :span="8">拼版中盒子的个数：
          <el-input v-model="form.pinbannum" type="name" style="width: 100%;max-width:200px;" placeholder="拼版中盒子的个数" @focus="numFocus" @blur="getPrice1()">0</el-input>
        </el-col>
      </el-form-item>
      <el-form-item label="是否对裱：">
        <el-col :span="8">
          <el-radio-group v-model="form.steps2" @change="checkradiu();getPrice1()">
            <el-radio label="是"/>
            <el-radio label="否"/>
          </el-radio-group>
        </el-col>
        <el-col :span="1" style="text-align:center;opacity:0">
          |
        </el-col>
        <el-col v-if="form.steps2=='是'" :span="8" class="line">裱纸类型：
          <el-cascader v-model="form.date2" :options="form.options2" placeholder="请选择裱纸类型" expand-trigger="hover" @change="changedate2();getPrice1()">2</el-cascader>
        </el-col><!-- <el-form-item :rules="[{ required: true, message: '年龄不能为空'},{ type: 'number', message: '年龄必须为数字值'}]" prop="name"></el-form-item> -->
      </el-form-item>
      <el-form-item label="选择面纸类型：">
        <el-col :span="8">
          <el-cascader v-model="form.date1" :options="form.options1" placeholder="请选择面纸类型" expand-trigger="hover" @change="changedate1();getPrice1()">1</el-cascader>
        </el-col>
        <el-col :span="1" style="text-align:center;opacity:0">
          |
        </el-col>
        <el-col :span="8" style="text-align:center;">
          成品数量：<el-input v-model="form.name" type="name" style="width: 100%;max-width:200px;" placeholder="请输入成品数量" @focus="numFocus" @blur="numBlur();getPrice1()" @keyup.native="proving1">0</el-input>
        </el-col>
        <!-- <el-col :span="8">
          <el-time-picker v-model="form.date2" type="fixed-time" placeholder="Pick a time" style="width: 100%;"/>
        </el-col> -->
      </el-form-item>
      <el-form-item label="选择印色：">
        <el-col :span="8">
          <el-select v-model="form.yinseType" placeholder="请选择印色类型" @change="getPrice1()">
            <el-option v-for="item in form.options4" :key="item.value" :label="item.label" :value="item.value">{{ item.label }}</el-option>
          </el-select>
        </el-col>
        <el-col :span="1" style="text-align:center;opacity:0">
          |
        </el-col>
        <!-- <el-col :span="8" style="text-align:center;">
          专色数量：<el-select v-model="form.zhuanseNum" placeholder="请选择专色" @change="getPrice1()">
            <el-option v-for="item in form.options3" :key="item.value" :label="item.label" :value="item.value">{{ item.label }}</el-option>
          </el-select>
        </el-col> -->
      </el-form-item>
      <el-form-item label="后工：">
        <el-col :span="5" class="fumo">
          <el-select v-model="form.fumoType" placeholder="选择覆膜" style="width:80%">
            <el-option v-for="item in form.options8" :key="item.value" :label="item.label" :value="item.value">{{ item.label }}</el-option>
          </el-select>
        </el-col>
        <el-col :span="5" class="fumo">
          刀版费用：
          <el-input v-if="true" v-model="form.daobanMoney" placeholder="单位：元" size="mini" style="width:80px;padding:0;text-align:center;">f</el-input>
        </el-col>
        <el-col :span="6" class="fumo" style="min-height:43px">
          <el-checkbox v-model="form.tangjinchecked" label="烫金" name="type"/>
          <el-input v-if="form.tangjinchecked" v-model="form.tangjinArr[0].l" placeholder="长cm" size="mini" style="width:65px;padding:0;text-align:center;" >f</el-input>
          <span v-if="form.tangjinchecked" style="display: inline-block;font-size: 20px;">×</span>
          <el-input v-if="form.tangjinchecked" v-model="form.tangjinArr[0].w" placeholder="宽cm" size="mini" style="width:65px;padding:0;text-align:center;">f</el-input>
          <el-button v-if="form.tangjinchecked" icon="el-icon-plus" size="mini" @click="addtangjinArr"/>
          <div v-for="(value,index) in form.tangjinArr" v-if="form.tangjinchecked&&index>0" :key="index">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&ensp;&ensp;&nbsp;&nbsp;&nbsp;
            <el-input v-model="value.l" placeholder="长cm" size="mini" style="width:65px;padding:0;text-align:center;">f</el-input>
            <span style="display: inline-block;font-size: 20px;">×</span>
            <el-input v-model="value.w" placeholder="宽cm" size="mini" style="width:65px;padding:0;text-align:center;">f</el-input>
            <el-button v-if="form.tangjinchecked" icon="el-icon-delete" size="mini" @click="deletetangjinArr(index)"/>
          </div>
        </el-col>
        <el-col :span="8" class="fumo" style="min-height:43px">
          <el-checkbox v-model="form.jituchecked" label="激凸" name="type"/>
          <el-input v-if="form.jituchecked" v-model="form.jituArr[0].l" placeholder="长cm" size="mini" style="width:65px;padding:0;text-align:center;">f</el-input>
          <span v-if="form.jituchecked" style="display: inline-block;font-size: 20px;">×</span>
          <el-input v-if="form.jituchecked" v-model="form.jituArr[0].w" placeholder="宽cm" size="mini" style="width:65px;padding:0;text-align:center;">f</el-input>
          <el-button v-if="form.jituchecked" icon="el-icon-plus" size="mini" @click="addjituArr"/>
          <div v-for="(value,index) in form.jituArr" v-if="form.jituchecked&&index>0" :key="index">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&ensp;&ensp;&nbsp;&nbsp;&nbsp;
            <el-input v-model="value.l" placeholder="长cm" size="mini" style="width:65px;padding:0;text-align:center;">f</el-input>
            <span style="display: inline-block;font-size: 20px;">×</span>
            <el-input v-model="value.w" placeholder="宽cm" size="mini" style="width:65px;padding:0;text-align:center;">fg</el-input>
            <el-button v-if="form.jituchecked" icon="el-icon-delete" size="mini" @click="deletejituArr(index)"/>
          </div>
        </el-col>
      </el-form-item>
      <el-form-item label="后工：">
        <el-col :span="5" class="fumo">
          <el-checkbox v-model="form.uvchecked" label="UV" name="type"/>&ensp;
          <el-input v-if="form.uvchecked" v-model="form.uvl" placeholder="长cm" size="mini" style="width:65px;padding:0;text-align:center;" >f</el-input>
          <span v-if="form.uvchecked" style="display: inline-block;font-size: 20px;">×</span>
          <el-input v-if="form.uvchecked" v-model="form.uvw" placeholder="宽cm" size="mini" style="width:65px;padding:0;text-align:center;">f</el-input>
        </el-col>
        <el-col :span="5" class="fumo">
          <el-checkbox v-model="form.guoyouchecked" label="过油" name="type"/>
        </el-col>
        <el-col :span="6" class="fumo" style="min-height:43px">
          <el-checkbox v-model="form.tianchuangchecked" label="天窗" name="type"/>
          <el-input v-if="form.tianchuangchecked" v-model="form.tianchuangArr[0].l" placeholder="长cm" size="mini" style="width:65px;padding:0;text-align:center;" >f</el-input>
          <span v-if="form.tianchuangchecked" style="display: inline-block;font-size: 20px;">×</span>
          <el-input v-if="form.tianchuangchecked" v-model="form.tianchuangArr[0].w" placeholder="宽cm" size="mini" style="width:65px;padding:0;text-align:center;">f</el-input>
          <el-button v-if="form.tianchuangchecked" icon="el-icon-plus" size="mini" @click="addtianchuangArr"/>
          <div v-for="(value,index) in form.tianchuangArr" v-if="form.tianchuangchecked&&index>0" :key="index">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&ensp;&ensp;&nbsp;&nbsp;&nbsp;
            <el-input v-model="value.l" placeholder="长cm" size="mini" style="width:65px;padding:0;text-align:center;">f</el-input>
            <span style="display: inline-block;font-size: 20px;">×</span>
            <el-input v-model="value.w" placeholder="宽cm" size="mini" style="width:65px;padding:0;text-align:center;">f</el-input>
            <el-button v-if="form.tianchuangchecked" icon="el-icon-delete" size="mini" @click="deletetianchuangArr(index)"/>
          </div>
        </el-col>
        <el-col :span="4" class="fumo">
          <!-- 粘盒 -->
          <el-select v-model="form.nianheType" placeholder="粘盒" @change="getPrice1()">
            <el-option v-for="item in form.options5" :key="item.value" :label="item.label" :value="item.value">{{ item.label }}</el-option>
          </el-select>
        </el-col>
      </el-form-item>
      <el-form-item label="后工：">
        <el-col :span="5" class="fumo">
          <!-- 手提绳 -->
          <el-select v-model="form.shoutishengType" placeholder="手提绳" style="width:80%">
            <el-option v-for="item in form.options6" :key="item.value" :label="item.label" :value="item.value">{{ item.label }}</el-option>
          </el-select>
        </el-col>
        <el-col :span="5" class="fumo">
          <el-checkbox v-model="form.yawenchecked" label="压纹" name="type"/>
        </el-col>
        <el-col :span="11" class="fumo">
          <el-checkbox v-model="form.dianbanchecked" label="垫板" name="type"/>
          <span v-if="form.dianbanchecked">尺寸（mm）：</span>
          <el-input v-if="form.dianbanchecked" v-model="form.boxl" placeholder="长" size="mini" style="width:60px;padding:0;text-align:center;" @change="pinbanChange();getPrice1()" >f</el-input>
          <span v-if="form.dianbanchecked" style="display: inline-block;font-size: 20px;">×</span>
          <el-input v-if="form.dianbanchecked" v-model="form.boxw" placeholder="宽" size="mini" style="width:60px;padding:0;text-align:center;" @change="pinbanChange();getPrice1()">f</el-input>
          <el-cascader v-if="form.dianbanchecked" v-model="form.dianbantype" :options="form.options11" placeholder="请选择垫板纸类型" expand-trigger="hover" @change="changedianban">8</el-cascader>
        </el-col>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="getPrice1"> 计算 </el-button>
        <el-button @click="onCancel">清空</el-button>
      </el-form-item>
    </el-form>
    <el-input v-model="textarea2" autosize type="textarea" placeholder="计算结果：" />
  </div>
</template>
<script>
export default {
  data() {
    return {
      textarea2: '',
      form: {
        name: '',
        // 是否对裱
        steps2: '',
        // 盒子尺寸-长宽高
        boxl: '',
        boxw: '',
        boxh: '',
        // 垫板的类型
        options11: [{
          value: '1',
          label: '白卡',
          children: [{
            value: '230',
            label: '230 g/m2'
          }, {
            value: '250',
            label: '250 g/m2'
          }, {
            value: '300',
            label: '300 g/m2'
          }, {
            value: '350',
            label: '350 g/m2'
          }]
        }, {
          value: '2',
          label: '灰板',
          children: [{
            value: '230',
            label: '230 g/m2'
          }, {
            value: '250',
            label: '250 g/m2'
          }, {
            value: '300',
            label: '300 g/m2'
          }, {
            value: '350',
            label: '350 g/m2'
          }]
        }],
        date1: [],
        // 面纸的类型
        options1: [{
          value: '1',
          label: '白卡',
          children: [{
            value: '230',
            label: '230 g/m2'
          }, {
            value: '250',
            label: '250 g/m2'
          }, {
            value: '300',
            label: '300 g/m2'
          }, {
            value: '350',
            label: '350 g/m2'
          }]
        }, {
          value: '2',
          label: '灰板',
          children: [{
            value: '230',
            label: '230 g/m2'
          }, {
            value: '250',
            label: '250 g/m2'
          }, {
            value: '300',
            label: '300 g/m2'
          }, {
            value: '350',
            label: '350 g/m2'
          }]
        }, {
          value: '3',
          label: '单面牛皮',
          children: [{
            value: '230',
            label: '230 g/m2'
          }, {
            value: '250',
            label: '250 g/m2'
          }, {
            value: '300',
            label: '300 g/m2'
          }, {
            value: '350',
            label: '350 g/m2'
          }]
        }, {
          value: '4',
          label: '国产牛皮',
          children: [{
            value: '250',
            label: '250 g/m2'
          }, {
            value: '300',
            label: '300 g/m2'
          }, {
            value: '350',
            label: '350 g/m2'
          }]
        }, {
          value: '5',
          label: '进口牛皮',
          children: [{
            value: '250',
            label: '250 g/m2'
          }, {
            value: '300',
            label: '300 g/m2'
          }, {
            value: '350',
            label: '350 g/m2'
          }]
        }],
        date2: [],
        // 表纸的类型
        options2: [{
          value: '1',
          label: '白卡',
          children: [{
            value: '230',
            label: '230 g/m2'
          }, {
            value: '250',
            label: '250 g/m2'
          }, {
            value: '300',
            label: '300 g/m2'
          }, {
            value: '350',
            label: '350 g/m2'
          }]
        }, {
          value: '2',
          label: '灰板',
          children: [{
            value: '230',
            label: '230 g/m2'
          }, {
            value: '250',
            label: '250 g/m2'
          }, {
            value: '300',
            label: '300 g/m2'
          }, {
            value: '350',
            label: '350 g/m2'
          }]
        }, {
          value: '3',
          label: '瓦楞纸',
          children: [{
            value: 'e-2.02',
            label: '5EW口杯纸，2.02元/㎡'
          }, {
            value: 'f-2.12',
            label: '5FW口杯纸，2.12元/㎡'
          }, {
            value: 'e-1.52',
            label: '5EB/W，1.52元/㎡'
          }, {
            value: 'e-1.65',
            label: '6EB/W，1.65元/㎡'
          }, {
            value: 'e-1.8元/㎡',
            label: '8EB/W，1.8元/㎡'
          }]
        }],
        // 白卡   5300元/吨 （后期可能会更改）灰板   4700元/吨 （后期可能会更改）单面牛皮  4500元/吨（后期可能会更改）国产牛皮  5500元/吨（后期可能会更改）进口牛皮  7000元/吨（后期可能会更改）
        unitPriceList: [5300, 4700, 4500, 5500, 7000],
        // 盒子的面积m⒉
        boxAreaList: [0, (254 / 1000 * 228 / 1000)],
        // 面纸的滚筒幅宽列表--进行对比--最佳幅宽
        // 白卡/灰板/单面牛皮：
        bestWlist: [350, 375, 400, 425, 450, 475, 500, 525, 550, 575, 600, 625, 650, 675, 700, 750, 800, 850, 900, 950, 1000, 1050, 1100],
        // 国产牛皮纸：
        bestWlist1: [393, 444, 546, 597, 787, 889, 1092],
        // 进口牛皮纸：
        bestWlist2: [400, 450, 500, 550, 600, 650, 700, 800, 900, 1000, 1100],
        // 白纸的损耗
        loss1: 0,
        // 裱纸的损耗
        loss2: 100,
        // 纸的钱=匹配幅宽后的纸张面积(m2)*克重 （g/m2）* 克价（元/g）*数量（拼版后纸张数量+损耗）
        price1: 0,
        // 印工的钱
        price2: 0,
        // 后工的钱
        price3: 0,
        // 专色
        options3: [{
          value: '1',
          label: '1专'
        }, {
          value: '2',
          label: '2专'
        }, {
          value: '3',
          label: '3专'
        }, {
          value: '4',
          label: '4专'
        }],
        // 印色
        yinseType: '',
        options4: [{
          value: '1',
          label: '4+0'
        }, {
          value: '2',
          label: '4+1'
        }, {
          value: '3',
          label: '0+2'
        }],
        // 粘盒
        nianheType: '',
        options5: [{
          value: '0',
          label: '无'
        }, {
          value: '1',
          label: '单粘'
        }, {
          value: '2',
          label: '对裱单粘口'
        }, {
          value: '3',
          label: '对裱双粘口'
        }, {
          value: '4',
          label: '勾底手工粘'
        }],
        // 拼版方式--双插盒
        options7: [{
          value: '1',
          label: '单拼（单排）'
        }, {
          value: '2',
          label: '双拼（单排）'
        }, {
          value: '4',
          label: '四拼（单排）'
        }, {
          value: '8',
          label: '四拼（双排）'
        }],
        // 手提绳
        shoutishengType: '',
        options6: [{
          value: '0',
          label: '无'
        }, {
          value: '1',
          label: '常规手提绳'
        }, {
          value: '2',
          label: '塑料提手'
        }],
        // 覆膜
        options8: [{
          value: '1',
          label: '无'
        }, {
          value: '2',
          label: '哑膜'
        }, {
          value: '3',
          label: '亮膜'
        }],
        zhuanseNum: '',
        delivery: false,
        type: [],
        // 展开的长度-宽高
        boxlenth: '',
        boxwidth: '',
        boxhight: '',
        // 匹配之后的纸的面积
        boxarea: '',
        desc: '',
        fumochecked: false,
        fumol: '',
        fumow: '',
        // 一张纸中有几个成品
        pinbanType: '',
        // 拼版中盒子的个数
        pinbannum: '',
        // 覆膜的类型 1-无覆膜，2-哑膜，3-亮膜
        fumoType: '',
        // 烫金的尺寸 长 宽 个数
        tangjinArr: [{
          l: '',
          w: ''
        }],
        tangjinnum: '',
        tangjinchecked: false,
        // 激凸的尺寸 长 宽 个数
        jituArr: [{
          l: '',
          w: ''
        }],
        jitunum: '',
        jituchecked: false,
        // 压纹
        yawenchecked: false,
        // uv的 长 宽
        uvl: '',
        uvw: '',
        uvchecked: false,
        // 天窗的尺寸 长 宽 个数
        tianchuangArr: [{
          l: '',
          w: ''
        }],
        tianchuangnum: '',
        tianchuangchecked: false,
        // 垫板
        dianbantype: [],
        // 把刀版的钱改成手动输入
        daobanMoney: ''
      },
      // 盒子的型号
      active: 1
    }
  },
  watch: {
    form: {
      handler(newName, oldName) {
        // console.log(newName.name + '" -- "' + oldName)
        // this.form.name = 10000
      },
      deep: true,
      immediate: true
    }
  },
  created: function() {
    // 对象不能比等
  },
  methods: {
    quchong(arr) {
      const arr1 = arr
      for (let index = 0; index < arr1.length; index++) {
        if (index + 1 === arr1.length) {
          continue
        }
        const element = arr1[index]
        const element1 = arr1[index + 1]
        if (element.l === element1.l && element.w === element1.w) {
          arr1.splice(index, 1)
        }
      }
      return arr1
    },
    addtianchuangArr() {
      // 增加烫金的个数--尺寸
      this.form.tianchuangArr.push({
        l: '',
        w: ''
      })
    },
    deletetianchuangArr(index) {
      // 删除天窗的个数--尺寸
      this.form.tianchuangArr.splice(index, 1)
    },
    addtangjinArr() {
      // 增加烫金的个数--尺寸
      this.form.tangjinArr.push({
        l: '',
        w: ''
      })
    },
    deletetangjinArr(index) {
      // 删除烫金的个数--尺寸
      this.form.tangjinArr.splice(index, 1)
    },
    addjituArr() {
      // 增加激凸的个数--尺寸
      this.form.jituArr.push({
        l: '',
        w: ''
      })
    },
    deletejituArr(index) {
      // 删除激凸的个数--尺寸
      this.form.jituArr.splice(index, 1)
    },
    checkradiu() {
      // 选择粘盒---单粘 （没有对裱纸及对裱工序）
    },
    proving1() {
      // 限制输入纸张数量为整数
      if (/[^\d]/g.test(this.form.name)) {
        this.form.name = this.form.name.replace(/[^\d]/g, '')
      }
    },
    numFocus() {
      // 限制输入纸张数量为整数
      if (this.form.name !== '') {
        this.form.name = this.form.name.split('个')[0]
      }
    },
    numBlur() {
      // 限制输入纸张数量为整数
      if (this.form.name !== '') {
        this.form.name = this.form.name + '个'
      }
    },
    hougongcheckbox() {
      console.log(this.form.type)
    },
    onSubmit() {
      this.$message('submit!')
    },
    imgSetActive(e) {
      // 让每个盒子类型被选中之后的效果
      this.active = e
    },
    getPrice1() {
      console.log(this.form.tangjinArr)
      // 后工被选择的数量
      var hougongArr = []
      // 对裱费用（对裱纸是白卡/灰板，单价是￥0.35/m2 ； 对裱纸是瓦楞： E楞￥0.35/m2 ， F楞￥0.4/m2）
      var duibiaoMoney = 0
      // 模切单价*拼版后纸张数量（ 起步价100元）1) 没有对裱工序 （没有对裱纸及对裱工序） ￥0.03/张 2) 有对裱工序 （白卡/灰板） ￥0.04/张 （瓦楞） ￥0.08/张
      var moqieMoney = 0
      var tangjinMoney = 0
      var fumoMoney = 0
      // if (this.form.pinbanType === '') {
      //   this.$message({
      //     message: '请选择拼版方式',
      //     type: 'warning'
      //   })
      //   return false
      // }
      // if (this.form.boxl === '' || this.form.boxw === '' || this.form.boxh === '') {
      //   this.$message({
      //     message: '请填写完整的长宽高',
      //     type: 'warning'
      //   })
      //   return false
      // }
      if (this.form.boxlenth === '' || this.form.boxwidth === '') {
        this.$message({
          message: '请填写计算后的尺寸',
          type: 'warning'
        })
        return false
      }
      console.log('面纸展开尺寸的宽：' + this.form.boxwidth)
      if (this.form.pinbannum === '') {
        this.$message({
          message: '请填写拼版中盒子的个数',
          type: 'warning'
        })
        return false
      }
      if (this.form.steps2 === '是') {
        if (this.form.date2.length === 0) {
          this.$message({
            message: '请填写裱纸的类型',
            type: 'warning'
          })
          return false
        }
      }
      if (this.form.date1.length === 0) {
        this.$message({
          message: '请填写面纸的类型',
          type: 'warning'
        })
        return false
      }
      if (this.form.name === '') {
        this.$message({
          message: '请填写成品数量',
          type: 'warning'
        })
        return false
      }
      var zhiNum = Number(this.form.name.split('个')[0]) / Number(this.form.pinbannum)
      // 匹配获得面纸和裱纸的面积
      var area1 = this.bestWlist(this.form.date1[0], this.form.date2[0])[0]
      // textarea2
      this.textarea2 = ''
      this.textarea2 += ('面纸选用滚筒的幅宽mm：' + this.bestWlist(this.form.date1[0], this.form.date2[0])[1] + '\n')
      console.log('面纸选用滚筒的幅宽mm：' + this.bestWlist(this.form.date1[0], this.form.date2[0])[1])
      console.log('面纸的面积：' + area1 + '拼版后纸的数量：' + zhiNum)
      this.textarea2 += ('面纸的面积：' + area1 + '   ' + '拼版后纸的数量：' + zhiNum + '\n')
      // 下面是印工的钱
      if (this.form.yinseType === '') {
        this.$message({
          message: '请选择印色',
          type: 'warning'
        })
        return false
      } else if (Number(this.form.yinseType) === 1) {
        // 400的基础上加70
        if (zhiNum <= 3000) {
          this.form.price2 = 400
        } else {
          this.form.price2 = 400 + Math.ceil((zhiNum - 3000) / 1000) * 70
        }
      } else if (Number(this.form.yinseType) === 2 || Number(this.form.yinseType) === 3) {
        // 400的基础上加70
        if (zhiNum <= 3000) {
          this.form.price2 = 800
        } else {
          this.form.price2 = 800 + Math.ceil((zhiNum - 3000) / 1000) * 100
        }
      }
      this.textarea2 += ('印工的钱: ' + this.form.price2 + '\n')
      console.log('印工的钱: ' + this.form.price2)
      let hougongMoney = 0
      if (this.form.fumoType === '' || this.form.fumoType === 1) {
        console.log('未选择覆膜')
      } else if (Number(this.form.fumoType) === 2) {
        fumoMoney = (area1 * 0.5 * zhiNum) <= 100 ? 100 : (area1 * 0.5 * zhiNum)
        this.textarea2 += ('覆膜的钱：' + fumoMoney + '\n')
        hougongMoney += parseFloat(fumoMoney)
      } else if (Number(this.form.fumoType) === 3) {
        fumoMoney = (area1 * 0.4 * zhiNum) <= 100 ? 100 : (area1 * 0.4 * zhiNum)
        this.textarea2 += ('覆膜的钱：' + fumoMoney + '\n')
        hougongMoney += parseFloat(fumoMoney)
      }
      // // 刀版的钱
      if (isNaN(Number(this.form.daobanMoney))) {
        this.$message({
          message: '请正确输入刀版的钱',
          type: 'warning'
        })
        return false
      }
      let hougongStr = ''
      if (this.form.daobanMoney) {
        hougongStr += ('刀版的钱' + this.form.daobanMoney + '\n')
        console.log('刀版的钱: ' + this.form.daobanMoney)
        hougongMoney += parseFloat(this.form.daobanMoney)
      }
      // 烫金的钱
      var banprice = 0
      let tangjinBlooen = false
      if (this.form.tangjinchecked) {
        // 循环遍历tangjinArr--去除相等
        for (let index = 0; index < this.form.tangjinArr.length; index++) {
          const element = this.form.tangjinArr[index]
          if (element.l === '' || element.w === '') {
            continue
          }
          tangjinBlooen = true
          const s = (parseFloat(element.l) + 1) * (parseFloat(element.w) + 1)
          if (s < 60) {
            tangjinMoney += 0.03
          } else {
            tangjinMoney += s * 0.0004
          }
          banprice += ((parseFloat(element.l) + 1) * (parseFloat(element.w) + 1) * 0.26) <= 20 ? 20 : ((parseFloat(element.l) + 1) * (parseFloat(element.w) + 1) * 0.26)
        }
        if (tangjinMoney <= 0.1) {
          tangjinMoney = 0.1 * zhiNum
        } else {
          tangjinMoney = tangjinMoney * zhiNum
        }
        if (tangjinBlooen) {
          hougongArr.push('tangjin')
          tangjinMoney = tangjinMoney + banprice
          console.log('烫金的钱: ' + tangjinMoney)
          hougongStr += ('烫金的钱: ' + tangjinMoney + '\n')
          hougongMoney += parseFloat(tangjinMoney)
        }
      }
      // 激凸的钱
      if (this.form.jituchecked) {
        var banprice1 = 0
        let jituBoolen = false
        var jituMoney = 0.3 * zhiNum
        // 循环遍历tangjinArr--去除相等
        for (let index = 0; index < this.form.jituArr.length; index++) {
          const element = this.form.jituArr[index]
          if (element.l === '' || element.w === '') {
            continue
          }
          jituBoolen = true
          banprice1 += ((parseFloat(element.l) + 1) * (parseFloat(element.w) + 1) * 0.26) <= 20 ? 20 : ((parseFloat(element.l) + 1) * (parseFloat(element.w) + 1) * 0.26)
        }
        if (jituBoolen) {
          hougongArr.push('jitu')
          jituMoney = jituMoney + banprice1
          console.log('激凸的钱: ' + jituMoney)
          hougongStr += ('激凸的钱: ' + jituMoney + '\n')
          hougongMoney += parseFloat(jituMoney)
        }
      }
      // 压纹的钱
      if (this.form.yawenchecked) {
        hougongArr.push('yawen')
        var yawenMoney = (0.06 * zhiNum) <= 100 ? 100 : (0.06 * zhiNum)
        console.log('压纹的钱: ' + yawenMoney)
        hougongStr += ('压纹的钱: ' + yawenMoney + '\n')
        hougongMoney += parseFloat(yawenMoney)
      }
      // UV的钱
      if (this.form.uvchecked) {
        if (this.form.uvl === '' || this.form.uvw === '') {
          this.$message({
            message: '请完整的输入UV尺寸',
            type: 'warning'
          })
          return false
        }
        hougongArr.push('uv')
        var uvMoney = ((parseFloat(this.form.uvl) * parseFloat(this.form.uvw) * 0.00025) <= 0.1 ? 0.1 : (parseFloat(this.form.uvl) * parseFloat(this.form.uvw) * 0.00025)) * zhiNum
        if (uvMoney <= 250) {
          uvMoney = 250
        }
        console.log('UV的钱: ' + uvMoney)
        hougongStr += ('UV的钱: ' + uvMoney + '\n')
        hougongMoney += parseFloat(uvMoney)
      }
      // 过油的钱
      if (this.form.guoyouchecked) {
        var guoyouMoney = (0.1 * zhiNum) <= 100 ? 100 : (0.1 * zhiNum)
        console.log('过油的钱: ' + guoyouMoney)
        hougongStr += ('过油的钱: ' + guoyouMoney + '\n')
        hougongMoney += parseFloat(guoyouMoney)
      }
      // 粘盒的钱
      var nianheMoney = 0
      if (this.form.nianheType === '' || Number(this.form.nianheType) === 0) {
        console.log('未选择粘盒')
      } else if (Number(this.form.nianheType) === 1) {
        nianheMoney = Number(this.form.name.split('个')[0]) > 20000 ? 0.02 * Number(this.form.name.split('个')[0]) : 0.05 * Number(this.form.name.split('个')[0])
        hougongStr += ('粘盒的钱: ' + nianheMoney + '\n')
        hougongMoney += parseFloat(nianheMoney)
      } else if (Number(this.form.nianheType) === 2) {
        nianheMoney = 0.1 * Number(this.form.name.split('个')[0])
        hougongStr += ('粘盒的钱: ' + nianheMoney + '\n')
        hougongMoney += parseFloat(nianheMoney)
      } else if (Number(this.form.nianheType) === 3) {
        nianheMoney = 0.16 * Number(this.form.name.split('个')[0])
        hougongStr += ('粘盒的钱: ' + nianheMoney + '\n')
        hougongMoney += parseFloat(nianheMoney)
      } else if (Number(this.form.nianheType) === 4) {
        nianheMoney = 0.07 * Number(this.form.name.split('个')[0])
        hougongStr += ('粘盒的钱: ' + nianheMoney + '\n')
        hougongMoney += parseFloat(nianheMoney)
      }
      console.log('粘盒的钱: ' + nianheMoney)
      // 天窗的钱
      if (this.form.tianchuangchecked) {
        var tianchuangMoney = 0
        let tianchuangBoolen = false
        for (let index = 0; index < this.form.tianchuangArr.length; index++) {
          const element = this.form.tianchuangArr[index]
          if (element.l === '' || element.w === '') {
            continue
          }
          tianchuangBoolen = true
          const s = parseFloat(element.l) * parseFloat(element.w)
          if (s <= 50) {
            tianchuangMoney += 0.1 * zhiNum
          } else if (s > 50 && s < 144) {
            tianchuangMoney += 0.15 * zhiNum
          } else {
            alert('天窗尺寸太大了！天窗的面积：' + s)
          }
        }
        if (tianchuangBoolen) {
          hougongStr += ('天窗的钱: ' + tianchuangMoney + '\n')
          hougongMoney += parseFloat(tianchuangMoney)
        }
      }
      console.log('天窗的钱: ' + tianchuangMoney)
      // 手提绳的钱
      if (Number(this.form.shoutishengType) === 1 || Number(this.form.shoutishengType) === 2) {
        var shoutishengMoney = (0.1 * zhiNum)
        console.log('手提绳的钱: ' + shoutishengMoney)
        hougongStr += ('手提绳的钱: ' + shoutishengMoney + '\n')
        hougongMoney += parseFloat(shoutishengMoney)
      }
      // 垫板的钱
      if (this.form.dianbanchecked) {
        if (this.form.boxl === '' || this.form.boxw === '') {
          this.$message({
            message: '请完整的垫板尺寸',
            type: 'warning'
          })
          return false
        }
        if (this.form.dianbantype.length === 0) {
          this.$message({
            message: '请选择垫板所用的材料',
            type: 'warning'
          })
          return false
        }
        var dianbanMoney = this.form.boxl * this.form.boxw * this.form.dianbantype[1] * this.form.unitPriceList[this.form.dianbantype[0] - 1] / 1000000 / 1000000 * Number(this.form.name.split('个')[0])
        console.log('垫板的钱: ' + dianbanMoney)
        hougongStr += ('垫板的钱: ' + dianbanMoney + '\n')
        hougongMoney += parseFloat(dianbanMoney)
      }
      let hougongName = ''
      if (hougongArr.indexOf('fumo') >= 0) {
        hougongName += ('覆膜、')
      }
      if (hougongArr.indexOf('tangjin') >= 0) {
        hougongName += ('烫金、')
      }
      if (hougongArr.indexOf('jitu') >= 0) {
        hougongName += ('激凸、')
      }
      if (hougongArr.indexOf('uv') >= 0) {
        hougongName += ('UV、')
      }
      if (hougongArr.indexOf('guoyou') >= 0) {
        hougongName += ('过油、')
      }
      if (hougongArr.indexOf('tianchuang') >= 0) {
        hougongName += ('天窗、')
      }
      if (hougongArr.indexOf('nianhe') >= 0) {
        hougongName += ('粘盒、')
      }
      if (hougongArr.indexOf('shoutisheng') >= 0) {
        hougongName += ('手提绳、')
      }
      if (hougongArr.indexOf('yawen') >= 0) {
        hougongName += ('压纹、')
      }
      if (hougongArr.indexOf('dianban') >= 0) {
        hougongName += ('垫板、')
      }
      hougongName = hougongName.substr(0, hougongName.length - 1)
      console.log('选择后工有：' + hougongName)
      // 面纸的损耗---(Number(this.form.yinseType) - 1)是专色数量
      var hougonglenth = hougongArr.length <= 1 ? 0 : Math.floor(hougongArr.length / 2) * 50
      this.form.loss1 = 150 + (this.form.steps2 !== '是' ? 0 : 50) + (Number(this.form.yinseType) - 1) * 50 + Math.ceil(zhiNum / 5000) * 50 + hougonglenth
      console.log('面纸的损耗：' + this.form.loss1)
      if (hougongName !== '') {
        this.textarea2 += ('选择后工有：' + hougongName + '\n')
      }
      this.textarea2 += ('面纸的损耗：' + this.form.loss1 + '\n')
      // const biaozhiMoney = this.data.form.boxAreaList * ( ?
      // 1、获取纸的钱
      // 1.1获取面纸的钱--通过克重获取对应的克价--
      // this.form.price1=this.data.form.boxAreaList * this.form.date1[1] * this.form.unitPriceList[this.form.date1[0] - 1] * (this.form.name.split('张')[0] + 面纸的损耗)
      if (this.form.steps2 !== '是') {
        // 如果不对裱
        this.form.price1 = area1 * this.form.date1[1] * this.form.unitPriceList[this.form.date1[0] - 1] / 1000000 * (zhiNum + this.form.loss1)
        console.log('面纸的价格:' + this.form.price1)
        this.textarea2 += ('面纸的价格' + this.form.price1 + '\n')
        // 模切的钱
        moqieMoney = 0.03 * zhiNum
      } else {
        // 模切的钱 （白卡/灰板） ￥0.04/张 （瓦楞） ￥0.08/张
        if (Number(this.form.date2[0]) === 1 || Number(this.form.date2[0]) === 2) {
          moqieMoney = 0.04 * zhiNum
        } else {
          moqieMoney = 0.08 * zhiNum
        }
        // 如果对裱--加上裱纸的钱
        this.form.price1 = area1 * this.form.date1[1] * this.form.unitPriceList[this.form.date1[0] - 1] / 1000000 * (zhiNum + this.form.loss1)
        console.log('面纸的价格:' + this.form.price1)
        this.textarea2 += ('面纸的价格' + this.form.price1 + '\n')
        // 1.2 获取裱纸的价格--分瓦楞纸和平常的纸
        // 滚筒的裱纸如果是滚筒的话--如果不是就不匹配滚筒用计算后的长宽相乘得面积
        let biaozhiMoney = 0
        if (Number(this.form.date2[0]) === 3) {
          biaozhiMoney = Number(this.form.boxwidth) * Number(this.form.boxlenth) / 1000000 * this.form.date2[1].split('-')[1] * (Number(this.form.name.split('个')[0]) + 100)
        } else {
          biaozhiMoney = this.biaozhibestWlist(this.form.date2[0])[0] * this.form.date2[1] / 1000000 * this.form.unitPriceList[this.form.date2[0] - 1] * (Number(this.form.name.split('个')[0]) + 100)
          console.log('裱纸选用滚筒的幅宽mm：' + this.biaozhibestWlist(this.form.date2[0])[1])
          this.textarea2 += ('裱纸选用滚筒的幅宽mm：' + this.biaozhibestWlist(this.form.date2[0])[1] + '\n')
        }
        console.log('裱纸的价格:' + biaozhiMoney)
        this.form.price1 = this.form.price1 + biaozhiMoney
        this.textarea2 += ('裱纸的价格' + biaozhiMoney + '\n')
        this.textarea2 += ('纸钱：' + this.form.price1 + '\n')
        // 对裱费用（对裱纸是白卡/灰板，单价是￥0.35/m2 ； 对裱纸是瓦楞： E楞￥0.35/m2 ， F楞￥0.4/m2）
        if (Number(this.form.date2[0]) === 1 || Number(this.form.date2[0]) === 2) {
          duibiaoMoney = this.biaozhibestWlist(this.form.date2[0])[0] * 0.35 * zhiNum
        } else if (this.form.date2[1].indexOf('e') >= 0) {
          duibiaoMoney = Number(this.form.boxwidth) * Number(this.form.boxlenth) / 1000000 * 0.35 * zhiNum
        } else if (this.form.date2[1].indexOf('f') >= 0) {
          duibiaoMoney = Number(this.form.boxwidth) * Number(this.form.boxlenth) / 1000000 * 0.4 * zhiNum
        }
        duibiaoMoney = duibiaoMoney <= 100 ? 100 : duibiaoMoney
        console.log('对裱费用:' + duibiaoMoney)
        this.textarea2 += ('对裱费用' + duibiaoMoney + '\n')
        hougongMoney += parseFloat(duibiaoMoney)
      }
      if (moqieMoney < 100) {
        moqieMoney = 100
      }
      console.log('模切的钱: ' + moqieMoney)
      this.textarea2 += ('模切的钱: ' + moqieMoney + '\n')
      hougongMoney += parseFloat(moqieMoney)
      this.textarea2 += hougongStr
      this.textarea2 += ('纸钱（面纸+对裱纸）+印工钱+后工=总成本=' + (this.form.price1 + hougongMoney + this.form.price2) + '\n')
      this.textarea2 += ('总金额/总成品数量*1.2= 报价 = ' + (this.form.price1 + hougongMoney + this.form.price2) / Number(this.form.name.split('个')[0]) * 1.2 + '\n')
    },
    changedate1(e) {
      // 让每个盒子类型被选中之后的效果
      // console.log(this.form.date1)
    },
    changedianban(e) {
      // 让每个盒子类型被选中之后的效果
      // console.log(this.form.dianbantype)
      // 垫板的钱
      if (this.form.dianbanchecked) {
        var dianbanMoney = this.form.boxl * this.form.boxw * this.form.dianbantype[1] * this.form.unitPriceList[this.form.dianbantype[0] - 1] / 1000000 / 1000000 * Number(this.form.name.split('个')[0])
      }
      console.log('垫板的钱' + dianbanMoney)
    },
    changedate2(e) {
      // 让每个盒子类型被选中之后的效果
      // console.log(this.form.date2)
    },
    pinbanChange(e) {
      // console.log(this.form.pinbanType)
      // 让每个盒子类型被选中之后的效果
      // console.log(this.active + '---' + this.form.boxl + '---' + this.form.boxw + '---' + this.form.boxh)
      if (this.form.boxl !== '' && this.form.boxw !== '' && this.form.boxh !== '') {
        this.totleArea(this.active, this.form.pinbanType)
      }
    },
    totleArea(boxType, pinbanType) {
      // 通过盒子的展开尺寸（长和宽）匹配最佳幅宽
      if (boxType === 1) {
        // 双插盒
        switch (Number(pinbanType)) {
          case 1:
          // 1、得出展开的长和宽展开长：(长+宽)*2+40---单位：毫米mm
            this.form.boxlenth = (parseFloat(this.form.boxl) + parseFloat(this.form.boxw)) * 2 + 40
            this.form.boxwidth = (20 + parseFloat(this.form.boxw)) * 2 + parseFloat(this.form.boxh) + 20
            console.log('单拼（单排）' + this.form.boxlenth + '---' + this.form.boxwidth)
            break
          case 2:
            this.form.boxlenth = (parseFloat(this.form.boxl) + parseFloat(this.form.boxw)) * 2 + 40
            this.form.boxwidth = (20 + parseFloat(this.form.boxw)) * 3 + 2 * parseFloat(this.form.boxh) + 20
            console.log('双拼（单排）')
            break
          case 4:
            this.form.boxlenth = (parseFloat(this.form.boxl) + parseFloat(this.form.boxw)) * 2 + 40
            this.form.boxwidth = (20 + parseFloat(this.form.boxw)) * 5 + 4 * parseFloat(this.form.boxh) + 20
            console.log('四拼（单排）')
            break
          case 8:
            this.form.boxlenth = [(parseFloat(this.form.boxl) + parseFloat(this.form.boxw)) * 2 + 20] + 20
            this.form.boxwidth = (20 + parseFloat(this.form.boxw)) * 3 + 2 * parseFloat(this.form.boxh) + 20
            console.log('四拼（双排）')
            break
          default:
            this.$message({
              message: '请选择拼版方式',
              type: 'warning'
            })
        }
        console.log(this.form.boxlenth + '---' + this.form.boxwidth)
        this.bestWlist(this.form.date1[0], this.form.date2[0])
      } else {
        this.$message({
          message: '需要增加其他的盒型计算展开尺寸',
          type: 'warning'
        })
      }
    },
    bestWlist(b) {
      // b表示面纸的类型
      // 匹配之后的纸的面积
      // 1/2/3白卡/灰板/单面牛皮：
      // 4国产牛皮纸 5进口牛皮纸
      var _this = this
      var a = Number(b)
      if (a === 1 || a === 2 || a === 3) {
        for (let index = 0; index < this.form.bestWlist.length; index++) {
          const element = _this.form.bestWlist[index]
          if (element - _this.form.boxwidth >= 0) {
            // 卷筒纸的每个纸的面积=幅宽 * 纸的长度 m2
            _this.form.boxarea = element * (_this.form.boxlenth) / 1000000
            return [_this.form.boxarea, element]
            // break
          }
        }
      } else if (a === 4) {
        console.log(this.form.bestWlist1)
        for (let index = 0; index < this.form.bestWlist1.length; index++) {
          const element = _this.form.bestWlist1[index]
          if (element - _this.form.boxwidth >= 0) {
            // 卷筒纸的每个纸的面积=幅宽 * 纸的长度 m2
            _this.form.boxarea = element * (_this.form.boxlenth) / 1000000
            return [_this.form.boxarea, element]
            // break
          }
        }
      } else if (a === 5) {
        for (let index = 0; index < this.form.bestWlist2.length; index++) {
          const element = _this.form.bestWlist2[index]
          if (element - _this.form.boxwidth >= 0) {
            // 卷筒纸的每个纸的面积=幅宽 * 纸的长度 m2
            _this.form.boxarea = element * (_this.form.boxlenth) / 1000000
            return [_this.form.boxarea, element]
            // break
          }
        }
      }
      this.$message({
        message: '没有匹配到面纸对应的滚筒幅宽',
        type: 'warning'
      })
    },
    biaozhibestWlist(b) {
      // b表示裱纸的类型
      // 匹配之后的纸的面积
      // 1/白卡2/灰板/3瓦楞
      var _this = this
      var a = Number(b)
      if (a === 1 || a === 2) {
        for (let index = 0; index < this.form.bestWlist.length; index++) {
          const element = _this.form.bestWlist[index]
          if (element - _this.form.boxlenth >= 0) {
            // 卷筒纸的每个纸的面积=幅宽 * 纸的长度 m2
            const area = element * (_this.form.boxwidth) / 1000000
            return [area, element]
            // break
          }
        }
      }
      this.$message({
        message: '没有匹配到裱纸对应的滚筒幅宽',
        type: 'warning'
      })
      return [0, 0]
    },
    onCancel() {
      this.$message({
        message: 'cancel!',
        type: 'warning'
      })
    }
  }
}
</script>

<style lang="scss"  type="text/css">
*{
  -webkit-user-select:none;

   -moz-user-select:none;

   -ms-user-select:none;

   user-select:none;
}
.line{
  text-align: center;
}
.imgList{
  text-align: center;
  li{
    margin-left: 20px;    margin-bottom: 22px;
    padding: 0 8px 6px 8px;
    display: flex;flex-direction:column;
    float: left;
    overflow: hidden;
    list-style-type: none!important;
    border-radius: 4px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, .12), 0 0 6px rgba(0, 0, 0, .04);
    border: 1px solid rgb(255,255,255);
    &:focus {
      outline: none;
    }
    &:hover{
      box-sizing: border-box;
      border: 1px solid rgb(255,103,1);
      box-shadow: 0 2px 4px rgba(255,103,1, .5), 0 0 6px rgba(255,103,1, .4);
    }
    & :first{
      margin-left: 0!important;
    }
    &.activeClass{
      box-sizing: border-box;
      border: 1px solid rgb(255,103,1);
      box-shadow: 0 2px 4px rgba(255,103,1, .5), 0 0 6px rgba(255,103,1, .4);
    }
  }
}
.fumo{
  &input{
    padding: 0;
    text-align: center;
  }
}
.showin-enter-active {
  display: block;
}
.showin-leave-active  {
  display: none;
  border-color: red;
}
</style>


<template>
    <div id="home">
        <div class="left">
            <el-menu
                default-active="1"
                class="el-menu-vertical-demo"
                @open="handleOpen"
                @close="handleClose"
                background-color="#545c64"
                text-color="#fff"
                active-text-color="#ffd04b">
                <template v-for="(item, i) in navList">
                    <el-submenu :index="item.index" :key="index">
                        <template slot="title">
                            <i :class="item.icon"></i>
                            <span>{{ item.name }}</span>
                        </template>
                        <template v-for="(subItem, j) in item.subMenu">
                            <el-menu-item :index="subItem.index" :key="subItem.key" @click="switchTab(subItem.key, subItem.name)">{{ subItem.name }}</el-menu-item>
                        </template>
                    </el-submenu>
                </template>
            </el-menu>
        </div>
        <div class="right">
            <el-container>
                <el-header>
                  <h3>{{ navContent.title }}</h3>
                  <div class="user-box">
                    <div>
                      <i class="el-icon-message-solid"></i>
                      <span>消息中心</span>
                    </div>
                    <div @click="() => this.$router.push('/login')">
                      <i class="el-icon-switch-button"></i>
                      <span>退出系统</span>
                    </div>
                    <div>
                      <i class="el-icon-user-solid"></i>
                      <span>个人中心</span>
                    </div>
                  </div>
                </el-header>
                <el-main>
                    <div class="filter-header">
                        <el-input :placeholder="showTableConfig.searchName" style="margin-right: 20px;"></el-input>
                        <el-button style="margin-right: 300px;">搜索</el-button>
                        <el-button type="primary">刷新</el-button>
                        <el-button type="primary">添加</el-button>
                    </div>
                    <div class="data-table">
                        <el-table
                            :data="showTableConfig.tableData"
                            style="width: 100%">
                            <tempalte v-for="(item, index) in showTableConfig.headers" :key="index">
                              <el-table-column
                                  :prop="item.prop"
                                  :label="item.label"
                                  :width="item.width">
                              </el-table-column>
                            </tempalte>
                            <el-table-column label="操作">
                              <template slot-scope="scope">
                                <el-button
                                    v-for="(item, index) in showTableConfig.operate"
                                    :type="item.type"
                                    size="mini">{{ item.name }}</el-button>
                              </template>
                            </el-table-column>
                        </el-table>
                        <el-pagination
                            background
                            layout="prev, pager, next"
                            :total="100"
                        ></el-pagination>
                    </div>
                </el-main>
            </el-container>
        </div>
    </div>
</template>

<script>
  export default {
    name: 'home',
    data: () => ({
      navList: [
          {
              name: '销售管理',
              index: '1',
              icon: 'el-icon-menu',
              subMenu: [
                  {
                      name: '客户信息管理',
                      index: '1-1',
                      key: 'customInfo',
                      icon: ''
                  },
                  {
                      name: '代理商管理',
                      index: '1-2',
                      key: 'agent'
                  },
                  {
                      name: '销售订单',
                      index: '1-3',
                      key: 'order'
                  },
              ]
          },
          {
              name: '计划管理',
              index: '2',
              icon: 'el-icon-s-flag',
              subMenu: [
                  {
                      name: '添加计划',
                      index: '2-1',
                      key: 'addPlan'
                  },
                  {
                      name: '计划实施',
                      index: '2-2',
                      key: 'doPlan'
                  }
              ]
          },
          {
              name: '财务管理',
              index: '3',
              icon: 'el-icon-s-custom',
              subMenu: [
                  {
                      name: '客户结算',
                      index: '3-1',
                      key: 'customPay'
                  },
                  {
                      name: '代理商结算',
                      index: '3-2',
                      key: 'agentPay'
                  },
                  {
                      name: '报销审批',
                      index: '3-3',
                      key: 'submitPay'
                  }
              ]
          },
          {
              name: '库存管理',
              index: '4',
              icon: 'el-icon-house',
              subMenu: [
                  {
                      name: '原材料',
                      index: '4-1',
                      key: 'material '
                  },
                  {
                      name: '库存管理',
                      index: '4-2',
                      key: 'inventory'
                  }
              ]
          },
          {
              name: '系统管理',
              index: '5',
              icon: 'el-icon-setting',
              subMenu: [
                  {
                      name: '用户管理',
                      index: '5-1',
                      key: 'user'
                  }
              ]
          }
      ],
      navContent: {
          title: '',
          tableHeaders: [],
          tableBtn: [],
          tableData: []
      },
      showTableConfig: {
        searchName: '',
        headers: [],
        tableData: [],
        operate: []
      },
      allTableData: {
        customInfo: {
          searchName: '请输入客户名称',
          headers: [
            {
              prop: 'name',
              label: '客户姓名',
              width: '250'
            },
            {
              prop: 'gender',
              label: '性别',
              width: '250'
            },
            {
              prop: 'number',
              label: '联系方式',
              width: '250'
            },
            {
              prop: 'address',
              label: '客户住址',
              width: '250'
            }
          ],
          tableData: [
            {
              name: '张三',
              gender: '男',
              number: '17126123123',
              address: '四川省成都市'
            },
            {
              name: '爱仕达',
              gender: '男',
              number: '17156123123',
              address: '四川省绵阳市'
            },
            {
              name: '阿斯达',
              gender: '男',
              number: '1712612423',
              address: '四川省凉山州'
            },
            {
              name: '阿斯达',
              gender: '男',
              number: '1712612423',
              address: '四川省凉山州'
            },
            {
              name: '阿斯达',
              gender: '男',
              number: '1712612423',
              address: '四川省凉山州'
            },
            {
              name: '阿斯达',
              gender: '男',
              number: '1712612423',
              address: '四川省凉山州'
            },
            {
              name: '阿斯达',
              gender: '男',
              number: '1712612423',
              address: '四川省凉山州'
            },
            {
              name: '阿斯达',
              gender: '男',
              number: '1712612423',
              address: '四川省凉山州'
            },
            {
              name: '阿斯达',
              gender: '男',
              number: '1712612423',
              address: '四川省凉山州'
            },
            {
              name: '阿斯达',
              gender: '男',
              number: '1712612423',
              address: '四川省凉山州'
            },
            {
              name: '阿斯达',
              gender: '男',
              number: '1712612423',
              address: '四川省凉山州'
            },
            {
              name: '阿1斯达',
              gender: '女',
              number: '1712612423',
              address: '四川省凉山州'
            },
            {
              name: '阿的达',
              gender: '女',
              number: '1756612423',
              address: '四川省凉山州'
            }
          ],
          operate: [
            {
              name: '删除',
              type: 'danger'
            },
            {
              name: '编辑',
              type: 'primary'
            },
            {
              name: '查看详情',
              type: 'success'
            }
          ]
        },
        agent: {
          searchName: '请输入代理商名称',
          headers: [
            {
              prop: 'agentName',
              label: '代理商',
              width: '300'
            },
            {
              prop: 'number',
              label: '电话',
              width: '300'
            },
            {
              prop: 'address',
              label: '公司住址',
              width: '300'
            }
          ],
          tableData: [
            {
              agentName: '张三',
              number: '17126123123',
              address: '四川省成都市'
            },
            {
              agentName: '张三',
              number: '17126123123',
              address: '四川省成都市'
            },
            {
              agentName: '张三',
              number: '17126123123',
              address: '四川省成都市'
            },
            {
              agentName: '张三',
              number: '17126123123',
              address: '四川省成都市'
            }
          ],
          operate: [
            {
              name: '删除',
              type: 'danger'
            },
            {
              name: '编辑',
              type: 'primary'
            },
            {
              name: '查看详情',
              type: 'success'
            }
          ]
        },
        order: {
          searchName: '请输入订单名称',
          headers: [
            {
              prop: 'orderNumber',
              label: '订单号',
              width: '200'
            },
            {
              prop: 'projectName',
              label: '项目名称',
              width: '150'
            },
            {
              prop: 'orderCount',
              label: '订单数量',
              width: '120'
            },
            {
              prop: 'unitPrice',
              label: '销售单价',
              width: '120'
            },
            {
              prop: 'totalPrice',
              label: '销售总额',
              width: '120'
            },
            {
              prop: 'receivePrice',
              label: '应收金额',
              width: '120'
            },
            {
              prop: 'payMethods',
              label: '付款方式',
              width: '120'
            },
            {
              prop: 'payPeople',
              label: '付款人',
              width: '120'
            },
            {
              prop: 'number',
              label: '联系方式',
              width: '120'
            }
          ],
          tableData: [
            {
              orderNumber: 'agd123126398124',
              projectName: '安徽省大',
              orderCount: '12',
              totalPrice: '12000',
              unitPrice: '120',
              receivePrice: '12000',
              payMethods: '银行卡转账',
              payPeople: '符合大赛',
              number: '1231234545'
            },
            {
              orderNumber: 'agd123126398124',
              projectName: '安徽省大',
              orderCount: '12',
              totalPrice: '12000',
              unitPrice: '120',
              receivePrice: '12000',
              payMethods: '银行卡转账',
              payPeople: '符合大赛',
              number: '1231234545'
            },
            {
              orderNumber: 'agd123126398124',
              projectName: '安徽省大',
              orderCount: '12',
              totalPrice: '12000',
              unitPrice: '120',
              receivePrice: '12000',
              payMethods: '银行卡转账',
              payPeople: '符合大赛',
              number: '1231234545'
            },
            {
              orderNumber: 'agd123126398124',
              projectName: '安徽省大',
              orderCount: '12',
              totalPrice: '12000',
              unitPrice: '120',
              receivePrice: '12000',
              payMethods: '银行卡转账',
              payPeople: '符合大赛',
              number: '1231234545'
            },
            {
              orderNumber: 'agd123126398124',
              projectName: '安徽省大',
              orderCount: '12',
              totalPrice: '12000',
              unitPrice: '120',
              receivePrice: '12000',
              payMethods: '银行卡转账',
              payPeople: '符合大赛',
              number: '1231234545'
            }
          ],
          operate: [
            {
              name: '删除',
              type: 'danger'
            },
            {
              name: '编辑',
              type: 'primary'
            },
            {
              name: '查看详情',
              type: 'success'
            }
          ]
        },
        addPlan: {
          searchName: '请输入计划名称',
          headers: [
            {
              prop: 'date',
              label: '时间',
              width: '200'
            },
            {
              prop: 'department',
              label: '部门',
              width: '150'
            },
            {
              prop: 'planDetail',
              label: '计划事项',
              width: '120'
            },
            {
              prop: 'startTime',
              label: '开始时间',
              width: '180'
            },
            {
              prop: 'endTime',
              label: '预期结束时间',
              width: '180'
            },
            {
              prop: 'joinDepartment',
              label: '涉及部门',
              width: '120'
            },
            {
              prop: 'head',
              label: '负责人',
              width: '120'
            }
          ],
          tableData: [
            {
              date: '2023-5-4 12:00',
              department: '人事部',
              planDetail: '发放工资',
              startTime: '2023-5-4 8:00',
              endTime: '2023-5-4 12:30',
              joinDepartment: '经理部',
              head: '包工头'
            },
            {
              date: '2023-5-4 12:00',
              department: '人事部',
              planDetail: '发放工资',
              startTime: '2023-5-4 8:00',
              endTime: '2023-5-4 12:30',
              joinDepartment: '经理部',
              head: '包工头'
            },
            {
              date: '2023-5-4 12:00',
              department: '人事部',
              planDetail: '发放工资',
              startTime: '2023-5-4 8:00',
              endTime: '2023-5-4 12:30',
              joinDepartment: '经理部',
              head: '包工头'
            },
            {
              date: '2023-5-4 12:00',
              department: '人事部',
              planDetail: '发放工资',
              startTime: '2023-5-4 8:00',
              endTime: '2023-5-4 12:30',
              joinDepartment: '经理部',
              head: '包工头'
            },
            {
              date: '2023-5-4 12:00',
              department: '人事部',
              planDetail: '发放工资',
              startTime: '2023-5-4 8:00',
              endTime: '2023-5-4 12:30',
              joinDepartment: '经理部',
              head: '包工头'
            }
          ],
          operate: [
            {
              name: '删除',
              type: 'danger'
            },
            {
              name: '编辑',
              type: 'primary'
            },
            {
              name: '查看详情',
              type: 'success'
            }
          ]
        },
        doPlan: {
          searchName: '请输入计划名称',
          headers: [
            {
              prop: 'date',
              label: '时间',
              width: '150'
            },
            {
              prop: 'department',
              label: '部门',
              width: '120'
            },
            {
              prop: 'planDetail',
              label: '计划事项',
              width: '120'
            },
            {
              prop: 'startTime',
              label: '开始时间',
              width: '150'
            },
            {
              prop: 'endTime',
              label: '预期结束时间',
              width: '150'
            },
            {
              prop: 'joinDepartment',
              label: '涉及部门',
              width: '120'
            },
            {
              prop: 'status',
              label: '实施状态',
              width: '120'
            },
            {
              prop: 'progress',
              label: '计划进度',
              width: '180'
            }
          ],
          tableData: [
            {
              date: '2023-5-4 12:00',
              department: '人事部',
              planDetail: '发放工资',
              startTime: '2023-5-4 8:00',
              endTime: '2023-5-4 12:30',
              joinDepartment: '经理部',
              status: '包工头',
              progress: '30%'
            },
            {
              date: '2023-5-4 12:00',
              department: '人事部',
              planDetail: '发放工资',
              startTime: '2023-5-4 8:00',
              endTime: '2023-5-4 12:30',
              joinDepartment: '经理部',
              status: '包工头',
              progress: '30%'
            },
            {
              date: '2023-5-4 12:00',
              department: '人事部',
              planDetail: '发放工资',
              startTime: '2023-5-4 8:00',
              endTime: '2023-5-4 12:30',
              joinDepartment: '经理部',
              status: '包工头',
              progress: '30%'
            },
            {
              date: '2023-5-4 12:00',
              department: '人事部',
              planDetail: '发放工资',
              startTime: '2023-5-4 8:00',
              endTime: '2023-5-4 12:30',
              joinDepartment: '经理部',
              status: '包工头',
              progress: '30%'
            },
            {
              date: '2023-5-4 12:00',
              department: '人事部',
              planDetail: '发放工资',
              startTime: '2023-5-4 8:00',
              endTime: '2023-5-4 12:30',
              joinDepartment: '经理部',
              status: '包工头',
              progress: '30%'
            }
          ],
          operate: [
            {
              name: '删除',
              type: 'danger'
            },
            {
              name: '编辑',
              type: 'primary'
            },
            {
              name: '查看详情',
              type: 'success'
            },
            {
              name: '更改状态',
              type: 'primary'
            }
          ]
        },
        customPay: {
          searchName: '请输入客户名称',
          headers: [
            {
              prop: 'name',
              label: '客户名',
              width: '200'
            },
            {
              prop: 'projectName',
              label: '费用项目名称',
              width: '150'
            },
            {
              prop: 'payDate',
              label: '收款日期',
              width: '120'
            },
            {
              prop: 'expectPay',
              label: '预收金额',
              width: '180'
            },
            {
              prop: 'actualPay',
              label: '实收金额',
              width: '180'
            },
            {
              prop: 'payMethods',
              label: '收款方式',
              width: '120'
            },
            {
              prop: 'residuePay',
              label: '项目结余',
              width: '120'
            },
            {
              prop: 'head',
              label: '经办人',
              width: '120'
            }
          ],
          tableData: [
            {
              name: '阿打算',
              projectName: '天河计划',
              payDate: '2023-5-5',
              expectPay: '231233',
              actualPay: '123123',
              payMethods: '银行卡转账',
              residuePay: '12323',
              head: '包工头'
            },
            {
              name: '阿打算',
              projectName: '天河计划',
              payDate: '2023-5-5',
              expectPay: '231233',
              actualPay: '123123',
              payMethods: '银行卡转账',
              residuePay: '12323',
              head: '包工头'
            },
            {
              name: '阿打算',
              projectName: '天河计划',
              payDate: '2023-5-5',
              expectPay: '231233',
              actualPay: '123123',
              payMethods: '银行卡转账',
              residuePay: '12323',
              head: '包工头'
            },
            {
              name: '阿打算',
              projectName: '天河计划',
              payDate: '2023-5-5',
              expectPay: '231233',
              actualPay: '123123',
              payMethods: '银行卡转账',
              residuePay: '12323',
              head: '包工头'
            },
            {
              name: '阿打算',
              projectName: '天河计划',
              payDate: '2023-5-5',
              expectPay: '231233',
              actualPay: '123123',
              payMethods: '银行卡转账',
              residuePay: '12323',
              head: '包工头'
            }
          ],
          operate: [
            {
              name: '删除',
              type: 'danger'
            },
            {
              name: '编辑',
              type: 'primary'
            },
            {
              name: '查看详情',
              type: 'success'
            }
          ]
        },
        agentPay: {
          searchName: '请输入代理商名称',
          headers: [
            {
              prop: 'agent',
              label: '代理商',
              width: '200'
            },
            {
              prop: 'projectName',
              label: '费用项目名称',
              width: '150'
            },
            {
              prop: 'payDate',
              label: '付款日期',
              width: '120'
            },
            {
              prop: 'expectPay',
              label: '预收金额',
              width: '180'
            },
            {
              prop: 'actualPay',
              label: '实收金额',
              width: '180'
            },
            {
              prop: 'payMethods',
              label: '收款方式',
              width: '120'
            },
            {
              prop: 'residuePay',
              label: '项目结余',
              width: '120'
            },
            {
              prop: 'head',
              label: '经办人',
              width: '120'
            }
          ],
          tableData: [
            {
              agent: '阿打算',
              projectName: '天河计划',
              payDate: '2023-5-5',
              expectPay: '231233',
              actualPay: '123123',
              payMethods: '银行卡转账',
              residuePay: '12323',
              head: '包工头'
            },
            {
              agent: '阿打算',
              projectName: '天河计划',
              payDate: '2023-5-5',
              expectPay: '231233',
              actualPay: '123123',
              payMethods: '银行卡转账',
              residuePay: '12323',
              head: '包工头'
            },
            {
              agent: '阿打算',
              projectName: '天河计划',
              payDate: '2023-5-5',
              expectPay: '231233',
              actualPay: '123123',
              payMethods: '银行卡转账',
              residuePay: '12323',
              head: '包工头'
            },
            {
              agent: '阿打算',
              projectName: '天河计划',
              payDate: '2023-5-5',
              expectPay: '231233',
              actualPay: '123123',
              payMethods: '银行卡转账',
              residuePay: '12323',
              head: '包工头'
            },
            {
              agent: '阿打算',
              projectName: '天河计划',
              payDate: '2023-5-5',
              expectPay: '231233',
              actualPay: '123123',
              payMethods: '银行卡转账',
              residuePay: '12323',
              head: '包工头'
            },
            {
              agent: '阿打算',
              projectName: '天河计划',
              payDate: '2023-5-5',
              expectPay: '231233',
              actualPay: '123123',
              payMethods: '银行卡转账',
              residuePay: '12323',
              head: '包工头'
            }
          ],
          operate: [
            {
              name: '删除',
              type: 'danger'
            },
            {
              name: '编辑',
              type: 'primary'
            },
            {
              name: '查看详情',
              type: 'success'
            }
          ]
        },
        submitPay: {
          searchName: '请输入报销申请事由',
          headers: [
            {
              prop: 'submitNumber',
              label: '报销单号',
              width: '150'
            },
            {
              prop: 'date',
              label: '日期',
              width: '150'
            },
            {
              prop: 'submitDepartment',
              label: '报销部门',
              width: '100'
            },
            {
              prop: 'submitThing',
              label: '申请事由',
              width: '120'
            },
            {
              prop: 'receiver',
              label: '收款人',
              width: '100'
            },
            {
              prop: 'bank',
              label: '开户行',
              width: '100'
            },
            {
              prop: 'account',
              label: '账号',
              width: '100'
            },
            {
              prop: 'money',
              label: '金额',
              width: '100'
            },
            {
              prop: 'head',
              label: '经办人',
              width: '100'
            },
            {
              prop: 'exam',
              label: '审批人',
              width: '100'
            }
          ],
          tableData: [
            {
              submitNumber: '1246547583123',
              date: '2023-5-4 12:00',
              submitDepartment: '开发部',
              submitThing: '怪怪的分公司',
              receiver: '梵蒂冈',
              bank: '中国银行',
              account: '12312312312412312312',
              money: '五万',
              head: '啊实打实',
              exam: '阿大声道'
            },
            {
              submitNumber: '1246547583123',
              date: '2023-5-4 12:00',
              submitDepartment: '开发部',
              submitThing: '怪怪的分公司',
              receiver: '梵蒂冈',
              bank: '中国银行',
              account: '12312312312412312312',
              money: '五万',
              head: '啊实打实',
              exam: '阿大声道'
            },
            {
              submitNumber: '1246547583123',
              date: '2023-5-4 12:00',
              submitDepartment: '开发部',
              submitThing: '怪怪的分公司',
              receiver: '梵蒂冈',
              bank: '中国银行',
              account: '12312312312412312312',
              money: '五万',
              head: '啊实打实',
              exam: '阿大声道'
            },
            {
              submitNumber: '1246547583123',
              date: '2023-5-4 12:00',
              submitDepartment: '开发部',
              submitThing: '怪怪的分公司',
              receiver: '梵蒂冈',
              bank: '中国银行',
              account: '12312312312412312312',
              money: '五万',
              head: '啊实打实',
              exam: '阿大声道'
            },
            {
              submitNumber: '1246547583123',
              date: '2023-5-4 12:00',
              submitDepartment: '开发部',
              submitThing: '怪怪的分公司',
              receiver: '梵蒂冈',
              bank: '中国银行',
              account: '12312312312412312312',
              money: '五万',
              head: '啊实打实',
              exam: '阿大声道'
            },
          ],
          operate: [
            {
              name: '删除',
              type: 'danger'
            },
            {
              name: '编辑',
              type: 'primary'
            },
            {
              name: '查看详情',
              type: 'success'
            }
          ]
        },
        inventory: {
          searchName: '请输入商品名称',
          headers: [
            {
              prop: 'date',
              label: '时间',
              width: '200'
            },
            {
              prop: 'goodsNumber',
              label: '商品单号',
              width: '150'
            },
            {
              prop: 'beginCount',
              label: '初期数',
              width: '120'
            },
            {
              prop: 'goodsName',
              label: '商品名称',
              width: '120'
            },
            {
              prop: 'price',
              label: '出库单价',
              width: '120'
            },
            {
              prop: 'outCount',
              label: '出库数量',
              width: '120'
            },
            {
              prop: 'inCount',
              label: '入库数量',
              width: '120'
            },
            {
              prop: 'sCount',
              label: '结余数',
              width: '120'
            },
            {
              prop: 'head',
              label: '经办人',
              width: '120'
            }
          ],
          tableData: [
            {
              date: '2023-5-4 12:00',
              goodsNumber: '1231242',
              beginCount: '23',
              goodsName: '显示屏',
              price: '500',
              outCount: '12',
              inCount: '23',
              sCount: '11',
              head: '阿斯达'
            },
            {
              date: '2023-5-4 12:00',
              goodsNumber: '1231242',
              beginCount: '23',
              goodsName: '显示屏',
              price: '500',
              outCount: '12',
              inCount: '23',
              sCount: '11',
              head: '阿斯达'
            },
            {
              date: '2023-5-4 12:00',
              goodsNumber: '1231242',
              beginCount: '23',
              goodsName: '显示屏',
              price: '500',
              outCount: '12',
              inCount: '23',
              sCount: '11',
              head: '阿斯达'
            },
            {
              date: '2023-5-4 12:00',
              goodsNumber: '1231242',
              beginCount: '23',
              goodsName: '显示屏',
              price: '500',
              outCount: '12',
              inCount: '23',
              sCount: '11',
              head: '阿斯达'
            },
            {
              date: '2023-5-4 12:00',
              goodsNumber: '1231242',
              beginCount: '23',
              goodsName: '显示屏',
              price: '500',
              outCount: '12',
              inCount: '23',
              sCount: '11',
              head: '阿斯达'
            }
          ],
          operate: [
            {
              name: '删除',
              type: 'danger'
            },
            {
              name: '编辑',
              type: 'primary'
            },
            {
              name: '查看详情',
              type: 'success'
            }
          ]
        },
        user: {
          searchName: '请输入用户名称',
          headers: [
            {
              prop: 'username',
              label: '用户名',
              width: '200'
            },
            {
              prop: 'role',
              label: '用户类型',
              width: '180'
            },
            {
              prop: 'department',
              label: '所属部门',
              width: '180'
            },
            {
              prop: 'position',
              label: '职位',
              width: '180'
            },
            {
              prop: 'createTime',
              label: '创建时间',
              width: '180'
            }
          ],
          tableData: [
            {
              username: '小芳',
              role: '管理员',
              department: '人事部',
              position: '人事',
              createTime: '2023-5-4 12:30'
            },
            {
              username: '小芳按时',
              role: '管理员',
              department: '人事部',
              position: '人事',
              createTime: '2023-1-4 12:30'
            },
            {
              username: '小强',
              role: '员工',
              department: '开发部',
              position: '前端开发',
              createTime: '2023-7-4 12:30'
            },
            {
              username: '小明',
              role: '超级管理员',
              department: '经理部',
              position: '副经理',
              createTime: '2023-1-4 12:30'
            },
            {
              username: '祥鸿',
              role: '员工',
              department: '后勤部',
              position: '后勤人员',
              createTime: '2023-6-4 12:30'
            },
          ],
          operate: [
            {
              name: '删除',
              type: 'danger'
            },
            {
              name: '编辑',
              type: 'primary'
            },
            {
              name: '查看详情',
              type: 'success'
            },
            {
              name: '修改权限',
              type: 'warning'
            }
          ]
        }
      }
    }),
    methods: {
      handleOpen(key, keyPath) {
        console.log(key, keyPath);
      },
      handleClose(key, keyPath) {
        console.log(key, keyPath);
      },
      switchTab(tab, name) {
        console.log(tab)
        this.navContent.title = name
        this.showTableConfig.headers = this.allTableData[tab].headers
        this.showTableConfig.tableData = this.allTableData[tab].tableData
        this.showTableConfig.operate = this.allTableData[tab].operate
        this.showTableConfig.searchName = this.allTableData[tab].searchName
      },
      handleEdit(index, row) {
        console.log(index, row);
      },
      handleDelete(index, row) {
        console.log(index, row);
      }
    }
  }
</script>

<style scoped lang="scss">
    #home{
        width: 100vw;
        height: 100vh;
        display: flex;
        align-items: center;
        justify-content: center;
        .left{
            width: 15%;
            height: 100%;
            background-color: #545c64;
        }
        .right{
            width: 85%;
            height: 100%;
            background-color: #fff;
            ::v-deep .el-container{
                width: 100%;
                height: 100%;
                .el-header{
                    background-color: #B3C0D1;
                    color: #333;
                    height: 10%;
                    display: flex;
                    align-items: center;
                    justify-content: space-between;
                    font-size: 22px;
                    font-weight: bold;
                  .user-box{
                    display: flex;
                    align-items: center;
                    justify-content: center;
                    div{
                      margin-right: 20px;
                      display: flex;
                      flex-direction: column;
                      align-items: center;
                      justify-content: center;
                      span{
                        font-size: 12px;
                      }
                      i{
                        cursor: pointer;
                      }
                    }
                  }
                }
                .el-main {
                    background-color: #E9EEF3;
                    color: #333;
                    height: 90%;
                    display: flex;
                    flex-direction: column;
                    align-items: center;
                    justify-content: center;
                }
            }
            .filter-header{
                width: 90%;
                height: 60px;
                display: flex;
                align-items: center;
                justify-content: flex-start;
                padding-left: 10px;
                padding-right: 10px;
                box-sizing: border-box;
                background-color: #B3C0D1;
            }
            .data-table{
                width: 90%;
                height: 800px;
                background-color: rgba(255, 255, 255, 0.7);
                display: flex;
                flex-direction: column;
                align-items: center;
                justify-content: center;
            }
        }
    }
</style>

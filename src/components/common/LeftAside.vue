<template>

  <el-scrollbar>
    <el-menu router :default-active="this.$route.path" class="el-menu-vertical-demo" background-color="#334157" text-color="#fff"
      active-text-color="#ffd04b" :collapse="showLeft" style="height: 1000px;">
      <el-menu-item index="/Main">
        <i class="el-icon-s-home"></i>
        <span slot="title">首页</span>
      </el-menu-item>
      <el-submenu v-for="me in menus" :key="'key-'+me.id" :index="'index'+me.id">
        <template slot="title">
          <i :class="me.icon"></i>
          <span>{{me.text}}</span>
        </template>
        <el-menu-item v-for="children in me.children" :key="'index-'+children.id" :index="children.url">
          {{children.text}}
        </el-menu-item>
      </el-submenu>
    </el-menu>
  </el-scrollbar>
</template>
<script>
  export default {
    props: ["showCollapsed"],
    data: function() {
      return {
        collapsed: true,
        menus: [{
            id: '1',
            text: '基础数据',
            icon: 'el-icon-tickets',
            children: [{
                id: '1-1',
                text: '收派标准',
                url: '/deliveryStandard'
              },
              {
                id: '1-2',
                text: '基础档案',
                url: '/basicArchives'
              },
              {
                id: '1-3',
                text: '班车设置',
                url: '/shuttleBusSet'
              },
              {
                id: '1-4',
                text: '取派设置',
                url: '/dispatchingPersonnelSet'
              },
              {
                id: '1-5',
                text: '区域设置',
                url: '/areaSet'
              },
              {
                id: '1-6',
                text: '管理分区',
                url: '/BasPartition'
              },
              {
                id: '1-7',
                text: '管理定区',
                url: '/BasZoneinfo'
              }
            ],
          },
          {
            id: '2',
            text: '权限管理',
            icon: 'el-icon-key',
            children: [{
                id: '2-1',
                text: '单位管理',
                url: '/UnitsManage'
              },
              {
                id: '2-2',
                text: '员工管理',
                url: '/EmpManage'
              },
              {
                id: '2-3',
                text: '栏目管理',
                url: '/columnManage'
              },
              {
                id: '2-4',
                text: '角色管理',
                url: ''
              }
            ]
          },
          {
            id: '3',
            text: '受理',
            icon: 'el-icon-takeaway-box',
            children: [{
                id: '3-1',
                text: '业务受理',
                url: '/businessAcceptance'
              },
              {
                id: '3-2',
                text: '工作单快速录入',
                url: '/worksheetQuickInput'
              },
              {
                id: '3-3',
                text: '工作单查询',
                url: '/worksheetQuery'
              }
            ]
          },
          {
            id: '4',
            text: '调度',
            icon: 'el-icon-view',
            children: [{
                id: '4-1',
                text: '查台转单',
                url: '/dispatch/CheckTableToTurnSingle'
              },
              {
                id: '4-2',
                text: '人工调度',
                url: '/dispatch/ArtificialScheduling'
              },
              {
                id: '4-3',
                text: '签收录入',
                url: '/dispatch/SignForEntry'
              },
              {
                id: '4-4',
                text: '取消签收申请确认',
                url: '/dispatch/CancelReceiptOfApplicationConfirmation'
              },
              {
                id: '4-5',
                text: '宣传任务',
                url: '/dispatch/PropagandaTask'
              }
            ]
          },
          {
            id: '5',
            text: '返货',
            icon: 'el-icon-document-copy',
            children: [{
                id: '5-1',
                text: '返货申请',
                url: '/returnthegoods/ReturnTheGoodsToApplyFor'
              },
              {
                id: '5-2',
                text: '返货申请确认',
                url: '/returnthegoods/ReturnRequestConfirmation'
              },
              {
                id: '5-3',
                text: '生成返货单',
                url: '/returnthegoods/GenerateAReturnNote'
              }
            ]
          },
          {
            id: '6',
            text: '包装材料管理',
            icon: 'el-icon-coin',
            children: [{
                id: '6-1',
                text: '包装材料物品管理',
                url: '/packagingMaterialManagement'
              },
              {
                id: '6-2',
                text: '入库管理',
                url: '/warehousingManagement'
              },
              {
                id: '6-3',
                text: '出库管理',
                url: '/outboundManagement'
              },
              {
                id: '6-4',
                text: '库存管理',
                url: '/inventoryManagement'
              }
            ]
          },
          {
            id: '7',
            text: '包装',
            icon: 'el-icon-soccer',
            children: [{
                id: '7-1',
                text: '包装信息录入',
                url: '/packagingInformationInput'
              },
              {
                id: '7-2',
                text: '包装信息查询',
                url: '/packagingInformationQuery'
              }
            ]
          },
          {
            id: '8',
            text: '大物流管理',
            icon: 'el-icon-apple',
            children: [{
              id: '8-1',
              text: '大物流发货对照表',
              url: '/iae/logistics'
            }]
          },
          {
            id: '9',
            text: '分拣管理',
            icon: 'el-icon-dessert',
            children: [{
                id: '9-1',
                text: '入库',
                url: '/storage'
              },
              {
                id: '9-2',
                text: '出库',
                url: '/theLibrary'
              },
              {
                id: '9-3',
                text: '盘库',
                url: '/check'
              },
              {
                id: '9-4',
                text: '合库',
                url: '/package'
              },
              {
                id: '9-5',
                text: '拆库',
                url: '/unpacking'
              },
              {
                id: '9-6',
                text: '出入库查询',
                url: '/outOfStorageQuery'
              },
              {
                id: '9-7',
                text: '库存查询',
                url: '/stockQuery'
              },
              {
                id: '9-8',
                text: '合包查询',
                url: '/packageQuery'
              },
              {
                id: '9-9',
                text: '单货异常监控',
                url: '/singleCargoExceptionMonitoring'
              }
            ]
          },
          {
            id: '10',
            text: '进出港管理',
            icon: 'el-icon-dish-1',
            children: [{
                id: '10-1',
                text: '出港配载',
                url: '/iae/IaeDeparture'
              },
              {
                id: '10-2',
                text: '提货管理',
                url: '/iae/IaeExtract'
              },
              {
                id: '10-3',
                text: '进港分单',
                url: '/iae/IaeArrival'
              },
              {
                id: '10-4',
                text: '出港配载查询',
                url: '/iae/Lineresource'
              },
              {
                id: '10-5',
                text: '到达时间录入',
                url: '/iae/IaeTimeinput'
              }
            ]
          },
          {
            id: '11',
            text: '物流管理',
            icon: 'el-icon-box',
            children: [{
                id: '11-1',
                text: '跟踪表登记',
                url: '/log/LogTrack'
              },
              {
                id: '11-2',
                text: '跟踪表查询',
                url: '/log/SelectLogTrack'
              },
              {
                id: '11-3',
                text: '物流交接单查询',
                url: '/log/LogLogisticstransfer'
              },
              {
                id: '11-4',
                text: '时间统计',
                url: '/log/Time'
              },
              {
                id: '11-5',
                text: '货量统计',
                url: '/log/LogLogistics'
              }
            ]
          }

        ]
      }
    },
    computed: {
      showLeft: function() {
        return this.showCollapsed;
      }
    }
  }
</script>
<style>
  .el-menu-vertical-demo:not(.el-menu--collapse) {
    width: 200px;
    min-height: 340px;

  }

  .el-scrollbar__wrap {
    overflow-x: hidden;
  }
</style>

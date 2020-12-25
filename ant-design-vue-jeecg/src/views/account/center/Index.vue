<!--个人中心页面-->
<template>
  <div class="page-header-index-wide page-header-wrapper-grid-content-main">

    <a-row :gutter="24">
      <a-col :md="24" :lg="7">
        <a-card :bordered="false">
          <div class="account-center-avatarHolder">
            <div class="avatar">
              <img :src="getAvatar()"/>
            </div>
            <div class="username">{{ nickname() }}</div>
            <div class="bio">个性签名</div>
          </div>
          <div class="account-center-detail">
            <p>
              <i class="title"></i>JAVA码农
            </p>
            <p>
              <i class="group"></i>中国邮政储蓄银行－软件研发中心－成都分中心
            </p>
            <p>
              <i class="address"></i><span>四川省</span><span>成都市</span>
            </p>
          </div>
          <a-divider />
          <a-divider :dashed="true" />
        </a-card>
      </a-col>
      <a-col :md="24" :lg="17">

      </a-col>
    </a-row>


  </div>
</template>

<script>
  import PageLayout from '@/components/page/PageLayout'
  import RouteView from "@/components/layouts/RouteView"
  import { AppPage, ArticlePage, ProjectPage } from './page'
  import { mapGetters } from 'vuex'
  import { getFileAccessHttpUrl } from '@/api/manage';

  export default {
    components: {
      RouteView,
      PageLayout,
      AppPage,
      ArticlePage,
      ProjectPage
    },
    data() {
      return {
        tags: ['很有想法的', '专注设计', '辣~', '大长腿', '川妹子', '海纳百川'],

        tagInputVisible: false,
        tagInputValue: '',

        teamSpinning: true,

        tabListNoTitle: [{
            key: 'article',
            tab: '文章(8)',
          }, {
            key: 'app',
            tab: '应用(8)',
          }, {
            key: 'project',
            tab: '项目(8)',
          }
        ],
        noTitleKey: 'app',
      }
    },
    mounted () {

    },
    methods: {
      ...mapGetters(["nickname", "avatar"]),
      getAvatar(){
          return getFileAccessHttpUrl(this.avatar());
      },

      handleTabChange (key, type) {
        this[type] = key
      },

      handleTagClose (removeTag) {
        const tags = this.tags.filter(tag => tag != removeTag)
        this.tags = tags
      },

      showTagInput () {
        this.tagInputVisible = true
        this.$nextTick(() => {
          this.$refs.tagInput.focus()
        })
      },

      handleInputChange (e) {
        this.tagInputValue = e.target.value
      },

      handleTagInputConfirm () {
        const inputValue = this.tagInputValue
        let tags = this.tags
        if (inputValue && tags.indexOf(inputValue) === -1) {
          tags = [...tags, inputValue]
        }

        Object.assign(this, {
          tags,
          tagInputVisible: false,
          tagInputValue: ''
        })
      }
    },
  }
</script>

<style lang="less" scoped>
  .page-header-wrapper-grid-content-main {
    width: 100%;
    height: 100%;
    min-height: 100%;
    transition: .3s;

    .account-center-avatarHolder {
      text-align: center;
      margin-bottom: 24px;

      & > .avatar {
        margin: 0 auto;
        width: 104px;
        height: 104px;
        margin-bottom: 20px;
        border-radius: 50%;
        overflow: hidden;
        img {
          height: 100%;
          width: 100%;
        }
      }

      .username {
        color: rgba(0, 0, 0, 0.85);
        font-size: 20px;
        line-height: 28px;
        font-weight: 500;
        margin-bottom: 4px;
      }
    }

    .account-center-detail {

      p {
        margin-bottom: 8px;
        padding-left: 26px;
        position: relative;
      }

      i {
        position: absolute;
        height: 14px;
        width: 14px;
        left: 0;
        top: 4px;
        background: url(https://gw.alipayobjects.com/zos/rmsportal/pBjWzVAHnOOtAUvZmZfy.svg)
      }

      .title {
        background-position: 0 0;
      }
      .group {
        background-position: 0 -22px;
      }
      .address {
        background-position: 0 -44px;
      }
    }

    .account-center-tags {
      .ant-tag {
        margin-bottom: 8px;
      }
    }

    .account-center-team {

      .members {
        a {
          display: block;
          margin: 12px 0;
          line-height: 24px;
          height: 24px;
          .member {
            font-size: 14px;
            color: rgba(0, 0, 0, .65);
            line-height: 24px;
            max-width: 100px;
            vertical-align: top;
            margin-left: 12px;
            transition: all 0.3s;
            display: inline-block;
          }
          &:hover {
            span {
              color: #1890ff;
            }
          }
        }
      }
    }

    .tagsTitle, .teamTitle {
      font-weight: 500;
      color: rgba(0,0,0,.85);
      margin-bottom: 12px;
    }

  }

</style>
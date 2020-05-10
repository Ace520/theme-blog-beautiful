<template>
  <footer class="footer">
    <div class="footer-con">
      <div class="footer-contact">
        <ul v-if="contact" class="contact">
          <li v-for="item in contact" :key="item.iconComponent" class="contact-item">
            <NavLink :link="item.link">
              <component :is="item.iconComponent"></component>
              {{ item.text }}
            </NavLink>
          </li>
        </ul>
      </div>

      <div class="footer-link">
        <div class="footer-link-item">
          <div>
            <div class="footer-link-item-title">推荐资源</div>
            <div>Yur - VuePress 主题</div>
            <div>Yur Cli - Yur 主题快速搭建工具</div>
          </div>
        </div>
        <div class="footer-link-item">
          <div>
            <div class="footer-link-item-title">相关信息</div>
            <div>本站托管于 CODING</div>
            <div>Yur Cli - Yur 主题快速搭建工具</div>
          </div>
        </div>
        <div class="footer-link-item">
          <div>
            <div class="footer-link-item-title">其它</div>
            <div>吐个槽</div>
            <div>社区交流扣群：686025154</div>
          </div>
        </div>
      </div>

      <div class="footer-copyright">
        <ul v-if="copyright" class="copyright">
          <li v-for="item in copyright" :key="item.text" class="copyright-item">
            <NavLink :link="item.link">{{ item.text }}</NavLink>
          </li>
        </ul>
      </div>
    </div>
  </footer>
</template>

<script>
import {
  CodepenIcon,
  CodesandboxIcon,
  FacebookIcon,
  GithubIcon,
  GitlabIcon,
  GlobeIcon,
  InstagramIcon,
  LinkedinIcon,
  MailIcon,
  MessageSquareIcon,
  MusicIcon,
  PhoneIcon,
  TwitterIcon,
  VideoIcon,
  YoutubeIcon,
} from 'vue-feather-icons'

export default {
  components: {
    CodepenIcon,
    CodesandboxIcon,
    FacebookIcon,
    GithubIcon,
    GitlabIcon,
    GlobeIcon,
    InstagramIcon,
    LinkedinIcon,
    MailIcon,
    MessageSquareIcon,
    MusicIcon,
    PhoneIcon,
    TwitterIcon,
    VideoIcon,
    YoutubeIcon,
  },

  computed: {
    contact() {
      return (
        (this.$themeConfig.footer && this.$themeConfig.footer.contact) ||
        []
      )
        .map(({ type, link }) => {
          return {
            iconComponent: this.getIconComponentName(type),
            link,
          }
        })
        .filter(({ iconComponent }) => iconComponent)
    },

    copyright() {
      return (
        (this.$themeConfig.footer && this.$themeConfig.footer.copyright) || []
      )
    },
  },

  methods: {
    getIconComponentName(contactType) {
      switch (contactType) {
        case 'codepen':
          return 'CodepenIcon'
        case 'codesandbox':
          return 'CodesandboxIcon'
        case 'facebook':
          return 'FacebookIcon'
        case 'github':
          return 'GithubIcon'
        case 'gitlab':
          return 'GitlabIcon'
        case 'instagram':
          return 'InstagramIcon'
        case 'linkedin':
          return 'LinkedinIcon'
        case 'mail':
          return 'MailIcon'
        case 'messenger':
          return 'MessageSquareIcon'
        case 'music':
          return 'MusicIcon'
        case 'phone':
          return 'PhoneIcon'
        case 'twitter':
          return 'TwitterIcon'
        case 'video':
          return 'VideoIcon'
        case 'web':
          return 'GlobeIcon'
        case 'youtube':
          return 'YoutubeIcon'
        default:
          return ''
      }
    },
  },
}
</script>

<style lang="stylus" scoped>
ol, ul {
  list-style: none;
  margin: 0;
  padding: 0;
}

.footer {
  box-sizing: border-box;
  background-color: $footerBgColor;
  display: flex;

  .footer-con {
    max-width: $contentWidth;
    margin: 0 auto;
    display: flex;
    flex-direction: column;
    flex: 1;
    align-items: center;
  }

  .footer-link {
    display: flex;
    justify-items: center;
    width: 100%;
    margin-bottom: 30px;
    margin-top: 15px;
    color: $footerColor;
    line-height: 30px;

    .footer-link-item {
      flex: 1;
      display: flex;
      align-items: center;
      justify-content: center;

      .footer-link-item-title {
        margin-bottom: 15px;
        font-size: 14px;
        border-bottom: 1px solid $footerColor;
        width: fit-content;
      }

      a {
        font-size: 12px;
        color: $footerColor;
        text-decoration: none;
        transition: color 0.3s;

        &:hover {
          color: #FFF;
        }
      }
    }
  }

  .footer-contact {
    margin: 20px;
    padding-top: 20px;
    text-align: center;
    line-height: 30px;
    flex: 1;
    display: flex;

    .contact {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;

      .contact-item {
        margin: 10px;

        a {
          font-size: 12px;
          color: $footerColor;
          text-decoration: none;
          transition: color 0.3s;

          &:hover {
            color: #FFF;
          }
        }
      }
    }
  }

  .footer-copyright {
    width: 100%;
    padding-top: 20px;
    border-top: 1px solid $footerColor;
    margin: 20px;
    display: flex;
    align-items: center;
    justify-content: center;

    @media (min-width: $MQNarrow) {
      justify-content: center;
    }

    .copyright {
      display: flex;
      justify-content: flex-end;

      .copyright-item {
        flex: 0 0 auto;
        padding: 0 10px;
        position: relative;
        line-height: 12px;
        border-right: 1px solid $footerColor;

        &:last-child {
          border-right: none;
        }

        a {
          font-size: 12px;
          color: $footerColor;
          text-decoration: none;
          transition: color 0.3s;

          &:hover {
            color: rgba(255, 255, 255, 0.9);
          }
        }
      }
    }
  }
}

@media (max-width: $MQMobile) {
  .footer {
    min-height: 100px;
    flex-direction: column;

    .footer-link {
      flex-direction: column;

      .footer-link-item {
        text-align: center;

        .footer-link-item-title {
          width: auto;
        }
      }
    }
  }
}
</style>

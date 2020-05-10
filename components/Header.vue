<template>
  <section id="header-wrapper">
    <header id="header">
      <div class="header-wrapper">
        <div class="title">
          <NavLink link="/" class="home-link">
            <svg
              height="30px"
              style="margin-top:12px;width:150px;"
              xmlns="http://www.w3.org/2000/svg"
            >
              <g>
                <text
                  font-size="20"
                  text-anchor="middle"
                  x="50%"
                  y="50%"
                  text-transform="uppercase"
                  fill="none"
                  stroke="#3498db"
                  text-shadow="0 0 1px #3498db"
                  stroke-width="1px"
                  stroke-dasharray="90 310"
                >
                  {{ $site.title }}
                  <animate
                    attributeName="stroke-dashoffset"
                    begin="-1.5s"
                    dur="6s"
                    from="0"
                    to="-400"
                    repeatCount="indefinite"
                  />
                </text>
                <text
                  font-size="20"
                  text-anchor="middle"
                  x="50%"
                  y="50%"
                  text-transform="uppercase"
                  fill="none"
                  stroke="#f39c12"
                  text-shadow="0 0 1px #f39c12"
                  stroke-width="1px"
                  stroke-dasharray="90 310"
                >
                  {{ $site.title }}
                  <animate
                    attributeName="stroke-dashoffset"
                    begin="-3s"
                    dur="6s"
                    from="0"
                    to="-400"
                    repeatCount="indefinite"
                  />
                </text>
                <text
                  font-size="20"
                  text-anchor="middle"
                  x="50%"
                  y="50%"
                  text-transform="uppercase"
                  fill="none"
                  stroke="#e74c3c"
                  text-shadow="0 0 1px #e74c3c"
                  stroke-width="1px"
                  stroke-dasharray="90 310"
                >
                  {{ $site.title }}
                  <animate
                    attributeName="stroke-dashoffset"
                    begin="-4.5s"
                    dur="6s"
                    from="0"
                    to="-400"
                    repeatCount="indefinite"
                  />
                </text>
                <text
                  font-size="20"
                  text-anchor="middle"
                  x="50%"
                  y="50%"
                  text-transform="uppercase"
                  fill="none"
                  stroke="#9b59b6"
                  text-shadow="0 0 1px #9b59b6"
                  stroke-width="1px"
                  stroke-dasharray="90 310"
                >
                  {{ $site.title }}
                  <animate
                    attributeName="stroke-dashoffset"
                    begin="-6s"
                    dur="6s"
                    from="0"
                    to="-400"
                    repeatCount="indefinite"
                  />
                </text>
              </g>
            </svg>
          </NavLink>
        </div>
        <SearchBox />
        <div class="header-right-wrap">
          <ul v-if="$themeConfig.nav" class="nav">
            <li v-for="item in $themeConfig.nav" :key="item.text" class="nav-item">
              <NavLink :link="item.link">{{ item.text }}</NavLink>
            </li>
          </ul>
        </div>
      </div>
    </header>
  </section>
</template>

<script>
import SearchBox from '@SearchBox'

export default {
  components: { SearchBox },
}
</script>

<style lang="stylus">
@import '~@app/style/config';

#header {
  top: 0;
  width: 100%;
  height: $headerHeight;
  box-sizing: border-box;
  padding: 20px 0;
  margin: auto;

  ol, ul {
    list-style: none;
    margin: 0;
    padding: 0;
  }
}

// border-bottom 5px solid lighten(#3eaf7c, 50%)
.header-wrapper {
  display: flex;
  line-height: 40px;
  height: 40px;
  max-width: $contentWidth;
  margin: 0 auto;

  .title {
    /* flex 0 0 200px */
    font-size: 18px;
    margin: 0;
    letter-spacing: 2px;
    display: block;
    text-transform: uppercase;

    a {
      color: $darkTextColor;
      font-weight: bold;
      font-family: PT Serif, Serif;
      text-decoration: none;
    }
  }

  .header-right-wrap {
    flex: 1;
    display: flex;
    justify-content: flex-end;
    align-items: center;

    .nav {
      flex: 0 0 auto;
      display: flex;
      margin: 0;

      .nav-item {
        margin-left: 20px;

        a {
          font-family: PT Serif, Serif;
          font-size: 18px;
          // color lighten(#3eaf7c, 30%)
          text-decoration: none;
          transition: color 0.3s;
        }
      }
    }

    .search-box {
      font-family: PT Serif, Serif;
      margin-left: 20px;

      input {
        border-radius: 5px;
        transition: all 0.5s;
        border: 1px solid #cecece;

        &:hover {
          border: 1px solid $accentColor;
          box-shadow: 0 0 5px $accentColor;
        }
      }

      .suggestions {
        border: 1px solid $darkBorderColor;
        top: 40px;
        right: 0;

        a {
          color: $darkTextColor;
          text-decoration: none;

          &.focused {
            color: $accentColor;
          }
        }
      }
    }
  }
}

@media (max-width: $MQMobile) {
  #header {
    display: none;
  }

  .header-wrapper {
    flex-direction: column;

    .header-right-wrap {
      display: none;
    }
  }
}
</style>

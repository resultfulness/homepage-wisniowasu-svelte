<div class="teampicker">
  <div class="teampicker-dropdown">
    <button class="teampicker-dropdown-button"
      >Zobacz SU z wybranego rocznika</button
    >
    <div class="teampicker-dropdown-content">
      <a href="/team/">2022/23</a>
      <a href="/team_2021_2022/">2021/22</a>
      <a href="/team_2020_2021/">2020/21</a>
      <a href="/team_2019_2020/">2019/20</a>
    </div>
  </div>
</div>

<style lang="scss">
  .teampicker {
    margin-top: 40px;

    &-dropdown {
      position: relative;
      display: block;
      margin: 0 auto;
      width: 280px;

      &::before {
        display: block;
        content: "";
        width: 100%;
        z-index: 3;
        background: linear-gradient(270deg, #ff7f66, #de1444);
        height: 2px;
        position: absolute;
      }

      &-button {
        background-color: white;
        box-shadow: 0 5px 10px 0 rgba(0, 0, 0, 0.1);
        border: none;
        border-radius: 0;
        color: rgba(0, 0, 0, 0.9);
        padding: 16px;
        font-size: 16px;
        position: relative;
        cursor: pointer;
        transition: background-color ease-in-out 0.1s,
          box-shadow ease-in-out 0.2s;
        width: 100%;
        z-index: 2;
      }

      &-content {
        transform: scaleY(0);
        transform-origin: top;
        opacity: 0;
        position: absolute;
        background-color: white;
        min-width: 280px;
        overflow-y: auto;
        box-shadow: 0 8px 16px 0 rgba(0, 0, 0, 0.2);
        margin: 0;
        z-index: 1;
        max-height: 200px;

        transition: transform ease-in-out 0.15s, opacity ease-in-out 0.1s;

        a {
          color: black;
          padding: 12px 16px;
          text-align: center;
          text-decoration: none;
          display: block;
          transition: background-color ease-in-out 0.1s;

          &:hover {
            background-color: whitesmoke;
          }
        }
      }

      &:hover {
        .teampicker-dropdown-content {
          transform: scaleY(1);
          opacity: 1;
        }

        .teampicker-dropdown-button {
          box-shadow: 0 0 15px 0 rgba(0, 0, 0, 0.2);
        }
      }
    }
  }
</style>

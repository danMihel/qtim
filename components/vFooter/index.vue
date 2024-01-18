<template>
  <div class="footer">
    <div class="footer-content">
      <span class="subtitle">Is there a project?</span>
      <div class="main-cocntent">
        <div>
          <div class="footer-title">Let’s work </div>
          <br>
          <div class="footer-title">together</div>
        </div>
        <div class="contacts">
          <div class="contacts-block">
            <p>
              For all questions
            </p>
            <div class="details">
              <a href="tel:+79202780068">+7 (920) 278—00—68</a>
              <a href="mailto:qtim@agency.com">qtim@agency.com</a>
            </div>
          </div>
          <div class="contacts-block">
            <p>
              Office in Russia
            </p>
            <div class="details">
              <span>139 Ruben Station Lake Drew, NM 52678</span>
              <telegramBtn class="telegram" />
            </div>
          </div>
          <div class="contacts-block">
            <p>
              Office in Dubai
            </p>
            <div class="details">
              <span>139 Ruben Station Lake Drew, NM 52678</span>
              <telegramBtn class="telegram" />
            </div>
          </div>
        </div>
        <div class="basement">
          <div class="links-container">
            <a href="">Facebook</a>
            <a href="">Instagram</a>
            <a href="">Telegram</a>
          </div>
          <div class="go-btn">
            <div class="go-text">GO</div>
          </div>
          <div class="links-container">
            <a href="">Behance</a>
            <a href="">Linkedn</a>
            <a href="">Privacy Policy</a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script setup lang="ts">
import telegramBtn from '@/components/UI/telegramBtn';
</script>
<style lang="scss">
.footer {
  margin-top: 140px;
  background-color: rgba(226, 190, 255, 1);

  .footer-content {
    margin-left: 112px;
    padding-top: 140px;

    .subtitle {
      font-size: 16px;
      line-height: 19.2px;

    }

    .main-cocntent {
      margin-top: 56px;
      display: grid;
      grid-template-columns: 3fr 2fr;

      .footer-title {
        width: fit-content;
        font-size: 112px;
        font-weight: 400;
        line-height: 112px;
        border-bottom: 1px solid currentColor;
        text-shadow:
          2px 2px rgba(226, 190, 255, 1),
          25px -2px rgba(226, 190, 255, 1),
          -25px 2px rgba(226, 190, 255, 1);
      }

      .contacts {
        font-size: 16px;
        line-height: 19.2px;
        display: flex;
        flex-direction: column;

        .contacts-block {
          margin-bottom: 36px;
          max-width: 152px;

          .details {
            display: flex;
            flex-direction: column;

            .telegram {
              margin-top: 8px;
            }
          }
        }
      }

      .basement {
        margin-top: 143px;
        bottom: 0;
        display: grid;
        grid-template-columns: repeat(3, 1fr);
        max-height: calc(358px / 2);
        grid-column: 1 / -1;
        overflow: hidden;
        place-items: center;

        .links-container {
          display: grid;
          grid-template-columns: repeat(3, 1fr);
          gap: 32px;
          max-width: 250px;
          margin-bottom: 60px;
          text-decoration: underline;
          text-underline-offset: 6px;
          text-size-adjust: calc(34px);
          white-space: nowrap;
        }

        .go-btn {
          color: rgba(243, 243, 243, 1);
          text-align: center;
          height: 358px;
          width: 358px;
          background-color: rgba(16, 16, 16, 1);
          border-radius: 50% 50% 0 0;

          .go-text {
            font-size: 32px;
            line-height: 32px;
            margin-top: calc((358px / 4) + 25px );
          }
        }
      }
    }
  }
}
</style>
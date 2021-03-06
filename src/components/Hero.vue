<template>
  <div class="hero">
    <header>
      <div class="overview">
        <h1>Theater Log</h1>
        <div class="overview-text">
          <p>
            Since watching Grease for the first time in 5th grade, I have been
            hooked on musicals! This app was built to keep track of all of the
            musicals and plays I have seen since 2010.
          </p>
          <p>
            Click on the show names to learn more about the show or current
            productions. And click on the song names to see a video of my
            favorite songs from each show!
          </p>
          <p class="portfolio-link">
            Created by
            <a href="https://musicalwebdev.com" target="_blank"
              >Brittany Walker.</a
            >
          </p>
        </div>
      </div>
      <div class="hero-sidebar">
        <div class="external-links">
          <h4>Other Logs</h4>
          <a href="https://thebookishlog.com" target="_blank">Bookish Log</a>
        </div>
        <div class="info">
          <ul>
            <li>
              <font-awesome-icon icon="star" class="fav-icon" /> = favorite
              shows
            </li>
            <li>
              <span class="multi-example">4</span> = times a show was seen
            </li>
          </ul>
        </div>
      </div>
    </header>
    <div class="statistics">
      <div class="statistics-content">
        <h3>Statistics</h3>
        <div class="stats">
          <div class="counter total-stat">
            <p class="stat-number">{{ shows.length + 26 }}</p>
            <p class="stat-title">Total Shows Seen</p>
          </div>
          <div class="counter upcoming-stat">
            <p class="stat-number">{{ upcomingCounter }}</p>
            <p class="stat-title">Upcoming</p>
          </div>
          <div class="counter musical-stat">
            <p class="stat-number">{{ musicalsCounter + 26 }}</p>
            <p class="stat-title">Musicals</p>
          </div>
          <div class="counter play-stat">
            <p class="stat-number">{{ playsCounter }}</p>
            <p class="stat-title">Plays</p>
          </div>
          <div class="counter price-stat">
            <p class="stat-number">${{ priceCounter.toLocaleString() }}</p>
            <p class="stat-title">Total Spent</p>
          </div>
          <div class="counter price-stat">
            <p class="stat-number">
              ${{ Math.floor(priceCounter / shows.length) }}
            </p>
            <p class="stat-title">Average Ticket Cost</p>
          </div>
        </div>
      </div>
      <div class="stats-sidebar">
        <div class="review-legend">
          <h3>Review Legend</h3>
          <ul class="review-emoji-list">
            <li>
              <img alt="love emoji" src="./../assets/love.svg" />
              <p>love</p>
            </li>
            <li>
              <img alt="happy emoji" src="./../assets/happy.svg" />
              <p>like</p>
            </li>
            <li>
              <img alt="funny emoji" src="./../assets/funny.svg" />
              <p>funny</p>
            </li>
            <li>
              <img alt="sad emoji" src="./../assets/sad.svg" />
              <p>sad</p>
            </li>
            <li>
              <img alt="confused emoji" src="./../assets/confused.svg" />
              <p>confused</p>
            </li>
            <li>
              <img alt="meh emoji" src="./../assets/meh.svg" />
              <p>meh</p>
            </li>
            <li>
              <img alt="dislike emoji" src="./../assets/dislike.svg" />
              <p>dislike</p>
            </li>
            <li>
              <img
                alt="happy but also sad emoji"
                src="./../assets/happy-sad.svg"
              />
              <p>sad but happy</p>
            </li>
            <li>
              <img
                alt="thought provoking emoji"
                src="./../assets/thought-provoking.svg"
              />
              <p>thought provoking</p>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { showList } from "../data/shows";

export default {
  name: "Hero",
  data: function() {
    return {
      shows: showList
    };
  },
  computed: {
    musicalsCounter: function() {
      var result = showList.reduce(
        (res, item) => (item.type == "musical" ? res + 1 : res),
        0
      );
      return result;
    },
    playsCounter: function() {
      var result = showList.reduce(
        (res, item) => (item.type == "play" ? res + 1 : res),
        0
      );
      return result;
    },
    upcomingCounter: function() {
      var result = showList.reduce(
        (res, item) => (item.upcoming ? res + item.upcoming : res),
        0
      );
      return result;
    },
    priceCounter: function() {
      var result = showList.reduce(
        (res, item) => (item.price ? res + item.price : res),
        0
      );
      return Math.floor(result);
    }
  }
};
</script>

<style lang="scss">
@import "@/assets/styles/variables.scss";
@import url("https://fonts.googleapis.com/css2?family=Abril+Fatface&display=swap");

.hero {
  header {
    border-bottom: 3px solid $black;
    @media screen and (min-width: 662px) {
      display: flex;
    }
    .overview {
      padding: 20px;
      display: flex;
      align-items: center;
      flex-wrap: wrap;
      @media screen and (min-width: 662px) {
        flex-basis: 75%;
        border-right: 3px solid $black;
      }
      h1 {
        font-family: "Abril Fatface", cursive;
        margin: 0;
        letter-spacing: 1.5px;
        font-size: 40px;
      }
    }
    .hero-sidebar {
      @media screen and (min-width: 662px) {
        width: 300px;
      }

      .external-links,
      .info {
        padding: 20px;
      }

      .external-links {
        border-top: 3px solid $black;
        border-bottom: 3px solid $black;
        a {
          padding: 5px 10px;
          background-color: $black;
          color: $purple;
          text-decoration: none;
          border: 3px solid $black;
        }
        a:hover {
          background-color: $purple;
          color: $black;
          transition: 0.5s;
        }
        @media screen and (min-width: 662px) {
          border-top: 0;
        }
      }

      .info {
        .fa-star {
          font-size: 24px;
        }
        .multi-example {
          border: 2px solid $black;
          padding: 5px;
          display: inline-block;
        }
        li:first-child {
          margin-bottom: 10px;
        }
        li {
          display: block;
        }
      }
    }
    .portfolio-link a {
      color: $black;
    }
  }
}

.statistics {
  border-bottom: 3px solid $black;
  .statistics-content {
    background-color: $black;
    color: $purple;
    padding: 20px;
    h3 {
      margin: 0;
    }
    .stats {
      display: flex;
      align-items: center;
      justify-content: center;
      flex-wrap: wrap;
      padding: 20px 0;
      @media screen and (min-width: 662px) {
        padding: 20px;
      }
      .counter {
        background-color: $purple;
        text-align: center;
        margin: 10px;
        border: 2px solid $purple;
        -webkit-box-shadow: 5px 5px 0 $purple;
        box-shadow: 9px 9px 0 $purple;
        border-radius: 7px;
        color: $black;
        outline: 3px solid $black;
        position: relative;
        .stat-number {
          font-size: 50px;
          font-weight: bold;
          margin: 0;
          padding: 10px 15px 0 15px;
        }
        .stat-title {
          margin: 0;
          padding: 0 15px 15px 15px;
        }
      }
    }
  }

  .review-legend {
    padding: 20px;
    border-top: 3px solid $black;
    text-align: center;
    .review-emoji-list {
      li {
        text-align: center;
        margin: 10px;
        p {
          border: 2px solid black;
          padding: 5px;
        }
        img {
          width: 40px;
        }
      }
    }
  }
}
</style>

<script lang="ts">
  import type { ServiceCardData } from "$lib/types";

  export let service: ServiceCardData;

  const { name, description, href, imgSrc, btnText, tag } = service;
</script>

<div class="service-card {tag}">
  <img data-src={imgSrc} class="logo lazyload" alt={name} />
  <div class="name">{name}</div>
  <div class="desc">{@html description}</div>
  <a {href} target="_blank" rel="noreferrer" class="btn">
    <span>{btnText}</span>
  </a>
</div>

<style lang="scss">
  $colour1: #ff7f66;
  $colour2: #de1444;

  .service-card {
    display: flex;
    flex-direction: column;
    flex-wrap: wrap;
    justify-content: flex-start;
    align-content: stretch;
    align-items: stretch;

    width: 300px;
    height: 400px;
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.3);
    margin: 20px;
    background-color: white;
    border-radius: 5px;

    > .logo {
      margin-top: 40px;
      width: 100px;
      height: 100px;
      object-fit: contain;
      align-self: center;
    }

    > .name {
      margin-top: 20px;
      font-size: 20px;
      align-self: center;
      font-family: "Raleway", sans-serif;
      text-transform: uppercase;
      font-weight: 700;
    }

    > .desc {
      margin: 20px;
      text-align: center;
    }

    > .btn {
      margin: auto auto 20px auto;
      font-family: "Poppins", sans-serif;
      text-transform: uppercase;
      font-weight: 600;
      font-size: 14px;
      display: block;
      text-decoration: none;
      border-radius: 50px;
      padding: 1em 3em;
      position: relative;
      color: rgba(255, 255, 255, 0.9);
      z-index: 0;
      transition: all 0.3s ease-in-out;
      cursor: pointer;
      background: linear-gradient(90deg, $colour1, $colour2);
    }

    > .btn::before {
      content: "";
      width: 100%;
      height: 100%;
      position: absolute;
      top: 0;
      left: 0;
      border-radius: 50px;
      z-index: -1;
      filter: blur(5px);
      opacity: 0.8;
      transition: all 0.3s ease-in-out;
      background: linear-gradient(90deg, $colour1, $colour2);
    }

    @media (hover: hover) {
      > .btn:hover {
        transform: scale(1.1);
      }

      > .btn:hover::before {
        filter: blur(10px);
        opacity: 0.9;
      }
    }

    &.soon > .btn {
      pointer-events: none;
      filter: grayscale(1);
    }

    &.new::before {
      content: "Nowe";
      position: absolute;
      width: 70px;
      height: 70px;
      text-align: center;
      vertical-align: middle;
      line-height: 70px;
      background-color: red;
      display: inline-block;
      z-index: 2;
      color: rgba(255, 255, 255, 0.9);
      box-shadow: 0 0 20px rgba(0, 0, 0, 0.2);
      font-family: "Poppins", sans-serif;
      text-transform: uppercase;
      font-weight: 600;
      font-size: 14px;
      border-radius: 50px;
      transform: rotate(-45deg) translate(0, -20px);
      background-image: linear-gradient(90deg, #ff512f, #dd2476);
    }

    &.soon::before {
      content: "Ju?? wkr??tce";
      position: absolute;
      width: 120px;
      height: 70px;
      text-align: center;
      vertical-align: middle;
      line-height: 70px;
      background-color: red;
      display: inline-block;
      z-index: 2;
      color: rgba(255, 255, 255, 0.9);
      box-shadow: 0 0 20px rgba(0, 0, 0, 0.2);
      font-family: "Poppins", sans-serif;
      text-transform: uppercase;
      font-weight: 600;
      font-size: 14px;
      border-radius: 50px;
      transform: translate(-40px, -5px) rotate(-45deg);
      background-image: linear-gradient(90deg, #ff512f, #dd2476);
    }
  }
</style>

<template>
  <div id="app">
    <Board />
    <footer class="zen-footer">
      <a class="zfo-logo" href="https://github.com/mhumph/zenboard"><span class="zfo-logo-dark">Zen</span><span class="zfo-logo-light">board</span></a>
      <span class="zfo-text">v0.4 | <a class="zfo-link" href="https://www.shutterstock.com/video/clip-12129530.html" target="_new">Beach loop &copy; Flixel Photos</a> | <a class="zfo-link" href="https://www.freepik.com/free-photos-vectors/icon" target="_new">Icon vector created by Freepik</a></span>
    </footer>
  </div>
</template>

<script>
import Board from './components/Board'

export default {
  name: 'App',
  components: {
    Board
  }
}
</script>

<style>
  html {
    /**
     * Copied from Boostrtap's normalize.css: Prevent iOS and IE text size 
     * adjust after device orientation change, without disabling user zoom.
     */
    -ms-text-size-adjust: 100%;
    -webkit-text-size-adjust: 100%;

  	font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
  }
  body {
    margin: 0;
  }
  #app {
    width: 100%;
  }

  /* Zen footer ***************************************************************/

  .zen-footer {
    text-align: center;
    margin: 15px;
  }
  .zen-footer a.zfo-logo {
    background-color: #fff;
    color: #FFF;
    font-size: 14px;
    text-decoration: none;
    padding: 2px 5px;
  }
  .zfo-logo-dark {
    color: #157d39; /* Alternatively, #38761d */
    font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
  }
  .zfo-logo-light {
    color: rgba(21,125,57,0.5);
    margin-left: 1px;
    font-family: 'HelveticaNeue-Light', 'Helvetica Neue Light', 'Helvetica Neue', Helvetica, Arial, sans-serif;
  }
  .zfo-text {
    color: #FFF;
    font-size: 12px;
    margin-left: 5px;
  }
  .zfo-link {
    color: #FFF;
    text-decoration: none;
  }

  /* Zen modal ****************************************************************/

  .zen-modal {
    position: fixed;
    z-index: 1;
    left: 0px;
    top: 0px;
    width: 100%;
    height: 100%;
    background-color: rgba(0,0,0,0.5);

    padding-top: 20px;
    overflow: auto; /* Enable scroll if needed */
  }
  .zmo-content {
    margin: 5% auto;
    width: 70%;
    max-width: 500px;
    padding: 15px 19px 15px 13px;
    background-color: #f9f9f9;
    border: 1px solid #CCC;
    font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;

    border-radius: 4px;
  }

  /* Zen form *****************************************************************/

  .zfo-title input {
    font-size: 23px;
    width: 100%;
    margin-bottom: 15px;

    border-width: 2px;
    padding: 4px;
    width: 99%;
  }
  .zfo-description textarea {
    width: 100%;
    height: 380px;
    margin-bottom: 10px;
    font-size: 16px;

    border-color: #CCC;
  }
  .zfo-archive {
    float: left;
    margin-top: 6px;
    margin-left: 21px;
    font-size: 13px;
  }

  /* Buttons */

  .zfo-buttons {
    text-align: right;
  }
  .zfo-button {
    background-color: #ddd;
    font-size: 13px;
    width: 80px;
    padding: 5px 20px;
    font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
  }
  .zfo-button:hover {
    background-color: #ccc;
  }
  .zfo-save {
    background-color: #209cee !important; /* Alternate value: #5de48c */
    color: #FFF;
  }
  .zfo-save:hover {
    background-color: #1190e3 !important;
  }
  .zfo-cancel {
    float: left;
  }
</style>

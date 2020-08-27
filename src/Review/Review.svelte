<script lang="ts">
  export let author;
  export let stars;
  export let review;
</script>

<style>
  .wrapper {
    display: flex;
    justify-content: flex-start;
    width: 55%;
  }

  .review {
    background-color: #f1e4e8;
    border-radius: 20px;
    padding: 20px;
    margin-top: 20px;
    display: flex;
    flex-direction: column;
    width: 100%;
    border-color: #b97375;
    box-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3), 4px 8px 14px rgba(0, 0, 0, 0.2);
  }

  span {
    font-size: 18px;
    padding-top: 8px;
  }
</style>

<div class="wrapper">
  <div class="review">
    <span>
      <b>Author:</b>
      {author}
    </span>
    <span>
      <b>Stars:</b>
      {stars}
    </span>
    <span>
      <b>Reviews:</b>
      {review}
    </span>
  </div>
</div>

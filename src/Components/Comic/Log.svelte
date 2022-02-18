<script>
   export let log
</script>

<li>
   <div class="upper">
      <div class="status">Reading</div>
      <div class="title">{log.title}</div>

      <div class="dates">
         <div class="update">Update: 2022-2-17</div>
         <div class="start">Start: 2021-12-17</div>
      </div>
   </div>

   <div class="lower">
      <div class="rank_dots">
         <div class="rank_dot"></div>
         <div class="rank_dot"></div>
         <div class="rank_dot"></div>
         <div class="rank_dot"></div>
         <div class="rank_dot"></div>
      </div>

      <div class="vol">vol.
         <span class="number">{log.number}</span>
      </div>

   </div>
</li>

<style>
    li {
        list-style: none;
        background: #fff;
        padding: 1.8rem 2rem;
    }

    .upper {
        display: flex;
        align-items: center;
        gap: 10px;
        margin-bottom: 1rem;
    }

    .status {
        font-size: 0.9rem;
        color: #666;
        width: 70px;
        background: #f6f6f6;
        border-radius: 6px;
        padding: 6px;
        text-align: center;
    }

    .title {
        color: #444;
        flex: 1;
    }

    .dates {
        color: #7c7c7c;
        font-size: 0.8rem;
        text-align: right;
    }

    .lower {
        display: flex;
        justify-content: space-between;
        align-items: end;
    }

    .vol {
        line-height: 1;
    }

    .number {
        font-size: 3rem;
    }

    .rank_dots {
        display: flex;
        gap: 0.3rem;
    }

    .rank_dot {
        width: 15px;
        height: 15px;
        background-color: #ccc;
        border-radius: 9999px;
    }

</style>

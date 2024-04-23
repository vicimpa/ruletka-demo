<script lang="ts">
  const rows: number[][] = [];
  const lastRow = ["1-18", "EVEN", "RED", "BLACK", "ODD", "19-36"];
  const rowsNum = ["st", "nd", "rd"];
  const reds = [1, 3, 7, 9, 12, 14, 16, 18, 19, 21, 23, 25, 27, 30, 32, 34, 36];

  for (let i = 0; i < 36; i++) {
    const j = 2 - (i % 3);
    const row = rows[j] ?? (rows[j] = []);
    row.push(i);
  }

  function* range(size: number) {
    for (let i = 0; i < size; i++) {
      yield i;
    }
  }
</script>

<table>
  <table>
    <tr>
      <td class="hide" />
      <td class="br1 br2 vGRAY" colspan={rows[0].length}>
        {'Рулетка "Красное-Черное"'}
      </td>
      <td class="hide" />
    </tr>
    {#each rows as row, i}
      <tr>
        {#each row as elem, j}
          {#if i === 0 && j === 0}
            <td class="row br1 br4 vGREEN" rowspan={3}>
              <span>0</span>
            </td>
          {/if}
          <td class={`elem ${reds.includes(elem + 1) ? "vRED" : "vBLACK"}`}>
            {elem + 1}
          </td>
          {#if (j + 1) % 12 === 0}
            <td class={`row vGREEN ${["br2", "", "br3"][i]}`}>
              <span>
                {2 - i + 1}{rowsNum[2 - i]}
              </span>
            </td>
          {/if}
        {/each}
      </tr>
    {/each}
    <tr>
      <t class="hide" />
      {#each range(rows[0].length / 4) as elem}
        <td class="vGRAY" colspan={4}>
          {elem * 12 + 1}
          -
          {(elem + 1) * 12}
        </td>
      {/each}
      <td class="hide" />
    </tr>
    <tr>
      <td class="hide" />
      {#each lastRow as elem, i}
        <td
          class={`vGRAY ${i == 0 ? "br4" : i == 5 ? "br3" : ""} v${elem}`}
          colspan={2}
        >
          {elem}
        </td>
      {/each}
      <td class="hide" />
    </tr>
  </table>
</table>

<style lang="scss">
  table {
    border-spacing: 0;
    border-collapse: separate;
  }

  td {
    text-align: center;
    box-shadow: 0 0 5px #000;
  }

  .vGRAY {
    color: #fff;
    background-color: gray;
  }

  .vGREEN {
    color: #fff;
    background-color: green;
  }
  .vRED {
    color: #fff;
    background-color: red;
  }
  .vBLACK {
    color: #fff;
    background-color: black;
  }

  .br1,
  .br2,
  .br3,
  .br4 {
    --b: 10px;
    --b1: 0;
    --b2: 0;
    --b3: 0;
    --b4: 0;

    border-radius: var(--b1) var(--b2) var(--b3) var(--b4);
  }

  .br1 {
    --b1: var(--b);
  }

  .br2 {
    --b2: var(--b);
  }

  .br3 {
    --b3: var(--b);
  }

  .br4 {
    --b4: var(--b);
  }

  .elem {
    width: 30px;
    height: 30px;
  }

  .row {
    text-align: center;
    vertical-align: middle;
    span {
      writing-mode: vertical-lr;
      transform: matrix(-1, 0, 0, -1, 0, 0);
    }
  }

  .hide {
    border: none;
    box-shadow: none;
  }
</style>

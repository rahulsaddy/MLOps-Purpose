![ols_forecasting_e2e_architecture](https://github.com/user-attachments/assets/4ef1a327-9e4a-482f-a5d3-f19078dee612)# MLOps-Purpose
MLOps flow for the MM forecasting



![Upload<svg width="100%" viewBox="0 0 680 860" xmlns="http://www.w3.org/2000/svg">
<defs>
  <marker id="arrow" viewBox="0 0 10 10" refX="8" refY="5" markerWidth="6" markerHeight="6" orient="auto-start-reverse">
    <path d="M2 1L8 5L2 9" fill="none" stroke="context-stroke" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
  </marker>
</defs>

<style>
  text { font-family: sans-serif; fill: #1a1a1a; }
  .th  { font-size: 14px; font-weight: 500; }
  .ts  { font-size: 12px; font-weight: 400; fill: #555; }
  .arr { stroke: #888; stroke-width: 1.5; fill: none; }

  .c-purple rect { fill: #EEEDFE; stroke: #534AB7; }
  .c-purple .th  { fill: #3C3489; }
  .c-purple .ts  { fill: #534AB7; }

  .c-coral rect  { fill: #FAECE7; stroke: #993C1D; }
  .c-coral .th   { fill: #712B13; }
  .c-coral .ts   { fill: #993C1D; }

  .c-teal rect   { fill: #E1F5EE; stroke: #0F6E56; }
  .c-teal .th    { fill: #085041; }
  .c-teal .ts    { fill: #0F6E56; }

  .c-amber rect  { fill: #FAEEDA; stroke: #854F0B; }
  .c-amber .th   { fill: #633806; }
  .c-amber .ts   { fill: #854F0B; }

  .c-gray rect   { fill: #F1EFE8; stroke: #5F5E5A; }
  .c-gray .th    { fill: #444441; }
  .c-gray .ts    { fill: #5F5E5A; }
</style>

<!-- Layer labels -->
<text class="ts" x="22" y="62"  writing-mode="tb" fill="#aaa">UI</text>
<text class="ts" x="22" y="148" writing-mode="tb" fill="#aaa">Validation</text>
<text class="ts" x="22" y="290" writing-mode="tb" fill="#aaa">Storage</text>
<text class="ts" x="22" y="460" writing-mode="tb" fill="#aaa">Modeling</text>
<text class="ts" x="22" y="650" writing-mode="tb" fill="#aaa">Insights</text>
<text class="ts" x="22" y="780" writing-mode="tb" fill="#aaa">Output</text>

<!-- LAYER 1: UI -->
<g class="c-purple">
  <rect x="200" y="30" width="280" height="54" rx="8" stroke-width="0.5"/>
  <text class="th" x="340" y="52" text-anchor="middle" dominant-baseline="central">Streamlit app</text>
  <text class="ts" x="340" y="70" text-anchor="middle" dominant-baseline="central">Analyst uploads marketing spend file</text>
</g>

<line x1="340" y1="84" x2="340" y2="112" class="arr" marker-end="url(#arrow)"/>

<!-- LAYER 2: VALIDATION -->
<g class="c-coral">
  <rect x="160" y="112" width="360" height="54" rx="8" stroke-width="0.5"/>
  <text class="th" x="340" y="134" text-anchor="middle" dominant-baseline="central">Pandera schema &amp; quality gate</text>
  <text class="ts" x="340" y="152" text-anchor="middle" dominant-baseline="central">Schema, nulls, ranges, duplicates</text>
</g>

<!-- fail branch -->
<line x1="160" y1="139" x2="80" y2="139" class="arr" stroke="#aaa" marker-end="url(#arrow)"/>
<g class="c-gray">
  <rect x="44" y="118" width="36" height="22" rx="4" stroke-width="0.5" opacity="0.7"/>
  <text class="ts" x="62" y="129" text-anchor="middle" dominant-baseline="central">fail</text>
</g>
<text class="ts" x="62" y="152" text-anchor="middle">Error shown</text>
<text class="ts" x="62" y="166" text-anchor="middle">in UI</text>

<line x1="340" y1="166" x2="340" y2="194" class="arr" marker-end="url(#arrow)"/>

<!-- LAYER 3: STORAGE -->
<rect x="50" y="194" width="580" height="160" rx="12" fill="none" stroke="#bbb" stroke-width="0.5" stroke-dasharray="5 3"/>
<text class="ts" x="62" y="210">Storage layer — DigitalOcean Spaces + PostgreSQL</text>

<g class="c-teal">
  <rect x="68" y="220" width="170" height="54" rx="8" stroke-width="0.5"/>
  <text class="th" x="153" y="242" text-anchor="middle" dominant-baseline="central">DO Spaces</text>
  <text class="ts" x="153" y="260" text-anchor="middle" dominant-baseline="central">Raw file (timestamped)</text>
</g>

<g class="c-teal">
  <rect x="255" y="220" width="170" height="54" rx="8" stroke-width="0.5"/>
  <text class="th" x="340" y="242" text-anchor="middle" dominant-baseline="central">Master dataset</text>
  <text class="ts" x="340" y="260" text-anchor="middle" dominant-baseline="central">Parquet / PostgreSQL</text>
</g>

<g class="c-teal">
  <rect x="442" y="220" width="170" height="54" rx="8" stroke-width="0.5"/>
  <text class="th" x="527" y="242" text-anchor="middle" dominant-baseline="central">Model artifacts</text>
  <text class="ts" x="527" y="260" text-anchor="middle" dominant-baseline="central">Versioned joblib on Spaces</text>
</g>

<line x1="260" y1="194" x2="153" y2="220" class="arr" stroke="#aaa" marker-end="url(#arrow)"/>
<line x1="340" y1="194" x2="340" y2="220" class="arr" stroke="#aaa" marker-end="url(#arrow)"/>
<line x1="340" y1="274" x2="340" y2="314" class="arr" marker-end="url(#arrow)"/>

<!-- LAYER 4: ANOMALY + MODELING -->
<g class="c-amber">
  <rect x="200" y="314" width="280" height="54" rx="8" stroke-width="0.5"/>
  <text class="th" x="340" y="336" text-anchor="middle" dominant-baseline="central">Anomaly detection</text>
  <text class="ts" x="340" y="354" text-anchor="middle" dominant-baseline="central">Flag outliers before retraining</text>
</g>

<line x1="340" y1="368" x2="340" y2="396" class="arr" marker-end="url(#arrow)"/>

<g class="c-purple">
  <rect x="160" y="396" width="360" height="54" rx="8" stroke-width="0.5"/>
  <text class="th" x="340" y="418" text-anchor="middle" dominant-baseline="central">Expanding window OLS retraining</text>
  <text class="ts" x="340" y="436" text-anchor="middle" dominant-baseline="central">scikit-learn, all data up to last week</text>
</g>

<!-- save model artifact arrow -->
<line x1="480" y1="423" x2="527" y2="274" class="arr" stroke="#aaa" stroke-dasharray="4 3" marker-end="url(#arrow)"/>
<text class="ts" x="535" y="360">save artifact</text>

<line x1="340" y1="450" x2="340" y2="478" class="arr" marker-end="url(#arrow)"/>

<g class="c-amber">
  <rect x="160" y="478" width="360" height="54" rx="8" stroke-width="0.5"/>
  <text class="th" x="340" y="500" text-anchor="middle" dominant-baseline="central">MLflow tracking</text>
  <text class="ts" x="340" y="518" text-anchor="middle" dominant-baseline="central">Coefficients, R², RMSE, anomaly flags</text>
</g>

<line x1="340" y1="532" x2="340" y2="560" class="arr" marker-end="url(#arrow)"/>

<!-- LAYER 5: PREDICTIONS + INSIGHTS -->
<g class="c-purple">
  <rect x="200" y="560" width="280" height="54" rx="8" stroke-width="0.5"/>
  <text class="th" x="340" y="582" text-anchor="middle" dominant-baseline="central">Prediction generation</text>
  <text class="ts" x="340" y="600" text-anchor="middle" dominant-baseline="central">Next week forecast from retrained model</text>
</g>

<line x1="340" y1="614" x2="340" y2="642" class="arr" marker-end="url(#arrow)"/>

<g class="c-coral">
  <rect x="160" y="642" width="360" height="54" rx="8" stroke-width="0.5"/>
  <text class="th" x="340" y="664" text-anchor="middle" dominant-baseline="central">Claude API — insight narration</text>
  <text class="ts" x="340" y="682" text-anchor="middle" dominant-baseline="central">Plain-English summary of model changes</text>
</g>

<!-- save predictions to Spaces -->
<line x1="480" y1="587" x2="596" y2="587" class="arr" stroke="#aaa" stroke-dasharray="4 3" marker-end="url(#arrow)"/>
<g class="c-teal">
  <rect x="596" y="566" width="66" height="42" rx="6" stroke-width="0.5"/>
  <text class="ts" x="629" y="583" text-anchor="middle" dominant-baseline="central">Predictions</text>
  <text class="ts" x="629" y="597" text-anchor="middle" dominant-baseline="central">on Spaces</text>
</g>

<line x1="340" y1="696" x2="340" y2="724" class="arr" marker-end="url(#arrow)"/>

<!-- LAYER 6: DASHBOARD -->
<g class="c-purple">
  <rect x="100" y="724" width="480" height="54" rx="8" stroke-width="0.5"/>
  <text class="th" x="340" y="746" text-anchor="middle" dominant-baseline="central">Streamlit dashboard</text>
  <text class="ts" x="340" y="764" text-anchor="middle" dominant-baseline="central">Predictions · diagnostics · insights · model health</text>
</g>

<!-- Legend -->
<rect x="50"  y="806" width="14" height="14" rx="3" fill="#EEEDFE" stroke="#534AB7" stroke-width="0.5"/>
<text class="ts" x="70"  y="817">Core pipeline</text>
<rect x="170" y="806" width="14" height="14" rx="3" fill="#E1F5EE" stroke="#0F6E56" stroke-width="0.5"/>
<text class="ts" x="190" y="817">Storage</text>
<rect x="260" y="806" width="14" height="14" rx="3" fill="#FAEEDA" stroke="#854F0B" stroke-width="0.5"/>
<text class="ts" x="280" y="817">Monitoring</text>
<rect x="370" y="806" width="14" height="14" rx="3" fill="#FAECE7" stroke="#993C1D" stroke-width="0.5"/>
<text class="ts" x="390" y="817">Intelligence</text>

</svg>
ing ols_forecasting_e2e_architecture.svg…]()

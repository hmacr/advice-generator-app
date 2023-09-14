<script lang="ts">
  import ImgDivider from '../assets/pattern-divider.svg';

  export let adviceNum: number;
  export let adviceContent: string;
</script>

<h3 class="text-sm text-neon-green uppercase tracking-[0.3em]">
  Advice #{adviceNum}
</h3>
<p class="font-extrabold text-2xl tracking-wide text-center">
  &#8220;{adviceContent}&#8221;
</p>
<img
  src={ImgDivider}
  alt="divider"
/>

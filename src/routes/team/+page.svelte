<script lang="ts">
  import TeamPage from "../TeamPage.svelte";

  import { management, chairpeople } from "$lib/content/team.json";
</script>

<TeamPage {management} {chairpeople} />

<script>
  import Header from "./components/Header.svelte";
  import Footer from "./components/Footer.svelte";
  import CreatePollForm from "./components/CreatePollForm.svelte";
  import PollList from "./components/PollList.svelte";
  import Tabs from "./shared/Tabs.svelte";

  //tabs
  let items = ["Current Polls", "Add New Poll"];
  let activeItem = "Current Polls";
  const tabChange = e => {
    activeItem = e.detail;
  };

  const handleAdd = data => {
    const poll = data.detail;
    polls = [poll, ...polls];
    activeItem = "Current Polls";
  };

  const handleVote = data => {
    const { id, option } = data.detail;

    let copiedPolls = [...polls];
    let upVotedPoll = copiedPolls.find(poll => id == poll.id);

    if (option === "a") {
      upVotedPoll.votesA++;
    } else {
      upVotedPoll.votesB++;
    }

    polls = copiedPolls;
  };

  let polls = [
    {
      id: 1,
      question: "Python or JavaScript?",
      answerA: "Python",
      answerB: "JavaScript",
      votesA: 9,
      votesB: 15
    }
  ];
</script>

<style>
  main {
    max-width: 960px;
    margin: 40px auto;
  }
</style>

<Header />
<main>
  <Tabs {activeItem} {items} on:tabChange={tabChange} />
  {#if activeItem === 'Current Polls'}
    <PollList {polls} on:vote={handleVote} />
  {:else}
    <CreatePollForm on:add={handleAdd} />
  {/if}
</main>
<Footer />

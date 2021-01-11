# Tree of Thoughts


## The Data Model

A message has a set of ports. These are "ports" in the GraphViz sense - a message can provoke multiple independent threads of reactions, each thread begins at, and is attached to, one port of the message node. 

Messages of one thread are attached to the same port. Ordering of messages, given the asynchronous nature of reality, is only inferred secondarily.

## Implementation

### App.svelte

```
<style>
	textarea { width: 100%; height: 2em; }
</style>
<script>
	let root = {body:"hello",threads:[
		{messages:[{body:'hi'}]},
		{messages:[{body:'hey'}]},
	]};
	let active = root;
</script>
	<div with it's own scrollbars>
		<Msg {root}/>
	</div>
	<textarea bind:value={text}></textarea>
```

### Msg.svelte
```
<script>
	export let root;
</script>
	<!-- side-by-side with flexbox or somesuch ( https://morioh.com/p/84b3ea38043c ): -->
	{#each root.threads as thread}
		<Thread root={thread}/>
	{#/each}

```

### Thread.svelte
```
% for rendering Markdown
import marked from 'marked';

export let root;

...

<div>{@html marked(root.body)}</div>

{#each root.messages as msg}
	
	<Msg root={msg}/>

{#/each}
```

## The Data Format

### RDF

#### why

#### beyond RDF - quads

#### conceptually, what's beyond quads?

#### anyway, JSON-LD, a practical format

It's easier to deal with the  JSON(-LD) format, where possible, even if our data are principially full RDF. JSON-LD is a useful standard for representing RDF as a JSON with some particularities. See FOL_solvers/json-ld/test1 for a little better  than the default choice of particularities. We'll omit the particularities fully for now, though.


---
# try also 'default' to start simple
theme: default
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
# some information about your slides (markdown enabled)
title: Model Context Protocol (MCP) for Scientific Software and Research Workflows
author: Simon Dürr
info: |
  ## Model Context Protocol (MCP) for Scientific Software and Research Workflows

# apply UnoCSS classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true

background: https://dev.simonduerr.eu/cover.png
---

<div class="flex justify-end items-center " >

<div class="w-1/3">

### Model Context Protocol (MCP) for Scientific Software and Research Workflows


<div @click="$slidev.nav.next" class="mt-12 py-1" hover:bg="white op-10">
  Press Space for next page <carbon:arrow-right />
</div>


<div class="flex space-x-4 mt-8">

<img src="/simon_duerr_face.jpg"  class="rounded-full w-20 h-20"/>
<div>
  <h6>Simon Dürr</h6>
  <span class="text-sm italic">
  Assistant Professor UAS<br>
  HES-SO Valais-Wallis<br>
  <a href="https://simonduerr.eu" target="_blank">simonduerr.eu</a><br>
  </span>
</div>
</div>

</div>
</div>


<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---
transition: fade-out
---

# Agenda

- Is AI making us more productive?
- What is the Model Context Protocol (MCP)?
- Examples of MCP for science
- How to create an MCP server



<!--
You can have `style` tag in markdown to override the style for the current page.
Learn more: https://sli.dev/features/slide-scope-style
-->

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>


---
layout: center
class: text-center
---

# Is AI making us more productive?

More productive developers should mean more code is released, no?

<img src="https://substackcdn.com/image/fetch/$s_!eBmO!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F4e23e3e0-d046-4b58-ab6d-bb8e78d38493_664x415.png" v-click>
<a href="https://mikelovesrobots.substack.com/p/wheres-the-shovelware-why-ai-coding"> Source </a>

---
layout: center
class: text-center
---

# Is it all not-open?

<img src="https://substackcdn.com/image/fetch/$s_!xhVj!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fd70b517d-c59b-4cb8-8b4f-7e5ee58f0424_632x568.png" class="h-[400px] w-auto " >

<a href="https://mikelovesrobots.substack.com/p/wheres-the-shovelware-why-ai-coding"> Source </a>
---
layout: center
class: text-center
---

# What is the Model Context Protocol (MCP)?

> USB-C for AI applications 

MCP offers a consistent protocol for linking AI models to external capabilities


---
layout: center
class: text-center
---

# M vs. N

Custom integrations for each new capability

![](https://huggingface.co/datasets/mcp-course/images/resolve/main/unit1/1.png)


---
layout: center
class: text-center
---

# MCP

Common protocol for all capabilities

![](https://huggingface.co/datasets/mcp-course/images/resolve/main/unit1/2.png)


---
layout: center
---

![](https://mintcdn.com/mcp/4ZXF1PrDkEaJvXpn/images/mcp-simple-diagram.png?fit=max&auto=format&n=4ZXF1PrDkEaJvXpn&q=85&s=9337f8096debc55621adcaf8ca563695)

[Source](https://modelcontextprotocol.io/docs/getting-started/intro)
---
layout: default
---

# Definitions

&nbsp;

### Host
- The user-facing AI application that end-users interact with directly e.g `Claude Desktop`, AI-enhanced IDEs like `Cursor`.
- Hosts initiate connections to MCP Servers and orchestrate the overall flow between user requests, LLM processing, and external tools.

### Client
- A component within the host application that manages communication with a specific MCP Server. 
- Each Client maintains a 1:1 connection with a single Server

### Server
- An external program or service that exposes capabilities (Tools, Resources, Prompts) via the MCP protocol.


<style>
h3 {
  background-color: #999;
  padding:0.2em;
  display: inline-block;
  color: white;
}
</style>
---
layout: center
class: text-center
---

# Type of capabilities 

<div class="grid grid-cols-2 gap-3">

<div class="rounded-lg p-1 bg-gradient-to-br from-blue-100 to-blue-300 shadow" v-click>
  
  ### Tools

  > Executable functions that the AI model can invoke to perform actions or retrieve computed data. Typically relating to the use case of the application.  
  
  <span class="text-sm"> ```def weather_in__location(lat, lng)```.</span>
</div>

<div class="rounded-lg p-1 bg-gradient-to-br from-green-100 to-green-300 shadow" v-click>
  
  ### Resources
  
  > Static or dynamic data that the AI model can access to inform its responses. Resources are typically read-only and provide context or background information relevant to the user’s query.  
  
  <span class="text-sm">  A database of drug information.</span>
</div>

<div class="rounded-lg p-1 bg-gradient-to-br from-yellow-100 to-yellow-300 shadow" v-click>

  ### Prompts

  > Predefined text snippets or templates that the AI model can use to structure its responses. Prompts help guide the model’s output to ensure it aligns with the desired format or style.  
  
  <span class="text-sm">  Template for responding to common customer inquiries. </span>
</div>

<div class="rounded-lg p-1 bg-gradient-to-br from-purple-100 to-purple-300 shadow" v-click>
  
  ### Sampling
  
  > Server-initiated requests for the Client/Host to perform LLM interactions, enabling recursive actions where the LLM can review generated content and make further decisions.  
  
 <span class="text-sm"> A writing application reviewing its own output and refining it further.</span>
</div>

</div>

---
layout: center
class: text-center
---

## Communication protocol

JSON-RPC 2.0 

![](https://huggingface.co/datasets/mcp-course/images/resolve/main/unit1/5.png)

stdio for local applications, HTTP+SSE for remote servers

---
layout: two-cols
---

## Tools

Tools are executable functions or actions that the AI model can invoke through the MCP protocol.

### Control
Tools are typically model-controlled, meaning that the AI model (LLM) decides when to call them based on the user’s request and context.

### Safety
Due to their ability to perform actions with side effects, tool execution can be dangerous. Therefore, they typically require explicit user approval.

::right::

<div class="flex items-center h-full">
```python
def get_weather(location: str) -> dict:
    """Get the current weather for a specified location."""
    # Connect to weather API and fetch data
    return {
        "temperature": 72,
        "conditions": "Sunny",
        "humidity": 45
    }
```
</div>

<style>
h3 {
  background-color: #999;
  padding:0.2em;
  display: inline-block;
  color: white;
}
</style>
---
layout: two-cols
---

## Resources

### Control
Resources are application-controlled, meaning the Host application typically decides when to access them.

### Nature
They are designed for data retrieval with minimal computation, similar to GET endpoints in REST APIs.

### Safety
read-only, lower security risks than `Tools`.

### Use Cases
- Access file contents
- Retrieve database records
- Read configuration information.

::right::

<div class="flex items-center h-full">
```python
def read_file(file_path: str) -> str:
    """Read the contents of a file at the specified path."""
    with open(file_path, 'r') as f:
        return f.read()
```
</div>

<style>
h3 {
  background-color: #999;
  padding:0.1em;
  display: inline-block;
  color: white;
  margin-bottom: -1em;
}
</style>
---
layout: two-cols
---  

## Prompts



### Control
Prompts are user-controlled, often presented as options in the Host application’s UI.

### Purpose
Structure interactions for optimal use of available Tools and Resources.

### Flow
Select a prompt before the AI model begins processing, setting context for the interaction.

### Use Cases
- Common workflows
- specialized task templates
- guided interactions

::right::

<div class="flex items-center h-full">

```python
def code_review(code: str, language: str) -> list:
    """Generate a code review for the provided code
     snippet."""
    return [
      {
          "role": "system",
          "content": f"You are a code reviewer examining
          {language} code. Provide a detailed review 
          highlighting best practices, potential issues,
          and suggestions for improvement."
      },
      {
          "role": "user",
          "content": f"Please review this {language} code:
          \n\n```{language}\n{code}\n```"
      }
    ]
```

</div>


<style>
h3 {
  background-color: #999;
  padding:0.2em;
  display: inline-block;
  color: white;
  margin-bottom: -1em;
}
</style>
---
layout: two-cols
---


## Sampling

### Control
Sampling is server-initiated but requires Client/Host facilitation.

### Purpose
Enables server-driven agentic behaviors and potentially recursive or multi-step interactions.

### Safety
Requires user approval due to the complexity and potential risks of multi-step tasks.

### Use Cases
 - Complex multi-step tasks
 - autonomous agent workflows
 - interactive processes.

::right::

```python
def request_sampling(messages, system_prompt=None, include_context="none"):
    """Request LLM sampling from the client."""
    # In a real implementation, this would send a request to the client
    return {
        "role": "assistant",
        "content": "Analysis of the provided data..."
    }
```

<div class="mt-6" v-click>
The sampling flow follows these steps:

1. Server sends a `sampling/createMessage` request to the client
2. Client reviews the request and can modify it
3. Client samples from an LLM
4. Client reviews the completion
5. Client returns the result to the server
</div>

<style>
h3 {
  background-color: #999;
  padding:0.2em;
  display: inline-block;
  color: white;
  margin-bottom: -1em;
}
</style>

---
layout: center
---

# Discovery process

One of MCP’s key features is dynamic capability discovery. When a Client connects to a Server, it can query the available Tools, Resources, and Prompts through specific list methods:

- `tools/list`: Discover available Tools
- `resources/list`: Discover available Resources
- `prompts/list`: Discover available Prompts


---
layout: center
---

```python
from mcp.server.fastmcp import FastMCP

# Create an MCP server
mcp = FastMCP("Weather Service")

# Tool implementation
@mcp.tool()
def get_weather(location: str) -> str:
    """Get the current weather for a specified location."""
    return f"Weather in {location}: Sunny, 72°F"

# Resource implementation
@mcp.resource("weather://{location}")
def weather_resource(location: str) -> str:
    """Provide weather data as a resource."""
    return f"Weather data for {location}: Sunny, 72°F"

# Prompt implementation
@mcp.prompt()
def weather_report(location: str) -> str:
    """Create a weather report prompt."""
    return f"""You are a weather reporter. Weather report for {location}?"""


# Run the server
if __name__ == "__main__":
    mcp.run()
```




---
layout: two-cols
---

# Limitations

### Tool Risk Levels
- Users may fall into patterns of auto-confirmation (YOLO mode)
- Sensitive data can be unintentionally exposed to third-party tools

### Cost Awareness
- Lack of controls for token efficiency can result in high costs for users.

### Unstructured Data
- Text-based outputs can lead to miscommunication or errors in critical tasks.

::right::


### Authentication challenges
- (Early versions lacked an authentication spec)
<br>

### Local code execution
- MCP servers can run locally, increasing the risk of malicious code execution.
<br>

### Trust issues
- Many servers trust inputs, leading to potential vulnerabilities.
- Dynamic tool redefinition can exploit user trust.

<style>
h3 {
  background-color: #999;
  padding:0.2em;
  display: inline-block;
  color: white;
  margin: 0.5em 0;
}
</style>


---
layout: center
---

# Case Study: Docker MCP



---
layout: center
---

# Case Study: Rosetta


<div class="flex items-center">
<div>
Scientific software for molecular modeling and analysis started in 2003 written in C++.

Can be controlled via RosettaScripts (XML-based scripting language) or PyRosetta (Python bindings).

Many different sources for documentation, tutorials, and examples: 
- Docs,  Issue Tracker + Github Issues, 2 forums, Slack

Significant tech debt (phd students come and go, code is not always well documented)


</div>
<div class="p-6">

Involved in the Chemistry Nobel Prize 2024 

![](/image-2.png){width="600px"}

</div>
</div>

---
layout: center
---

# Rosetta MCP Server

<a href="https://github.com/Arielbs/rosetta-mcp-server"> Rosetta MCP Server </a>

---
layout: center
---

# Case Study: MCP for Mechanistic Modelling
&nbsp;

![](/image.png){width="600px"}
[Source](https://www.biorxiv.org/content/10.1101/2025.09.10.675105v2.full.pdf)


---
layout: center
---

# In practice
&nbsp;

![alt text](/image-1.png)
[Source](https://www.biorxiv.org/content/10.1101/2025.09.10.675105v2.full.pdf)

---
layout: center
---

# Awesome MCP Servers


- [genomoncology/biomcp](https://github.com/genomoncology/biomcp) - Biomedical research MCP server providing access to PubMed, ClinicalTrials.gov, and MyVariant.info.
- [longevity-genie/biothings-mcp](https://github.com/longevity-genie/biothings-mcp) - MCP server to interact with the BioThings API, including genes, genetic variants, drugs, and taxonomic information.
- [longevity-genie/gget-mcp](https://github.com/longevity-genie/gget-mcp)  - MCP server providing a powerful bioinformatics toolkit for genomics queries and analysis, wrapping the popular `gget` library.
- [wso2/fhir-mcp-server](https://github.com/wso2/fhir-mcp-server)  - Model Context Protocol server for Fast Healthcare Interoperability Resources (FHIR) APIs. Provides seamless integration with FHIR servers, enabling AI assistants to search, retrieve, create, update, and analyze clinical healthcare data with SMART-on-FHIR authentication support.
- [JamesANZ/medical-mcp](https://github.com/JamesANZ/medical-mcp)  - An MCP server that provides access to medical information, drug databases, and healthcare resources. Enables AI assistants to query medical data, drug interactions, and clinical guidelines.


[Awesome MCP Servers](https://github.com/punkpeye/awesome-mcp-servers)

---
layout: center
---

# Tools for building MCP servers 

- [fastmcp](https://gofastmcp.com/getting-started/welcome)
- [gradio](https://www.gradio.app/guides/building-mcp-server-with-gradio)

---
layout: center
---

# Gradio MCP 

<div class="overflow-y-auto h-[400px]">
```python
import gradio as gr

def letter_counter(word, letter):
    """
    Count the number of occurrences of a letter in a word or text.

    Args:
        word (str): The input text to search through
        letter (str): The letter to search for

    Returns:
        str: A message indicating how many times the letter appears
    """
    word = word.lower()
    letter = letter.lower()
    count = word.count(letter)
    return count

demo = gr.Interface(
    fn=letter_counter,
    inputs=[gr.Textbox("strawberry"), gr.Textbox("r")],
    outputs=[gr.Number()],
    title="Letter Counter",
    description="Enter text and a letter to count how many times the letter appears in the text."
)

if __name__ == "__main__":
    demo.launch(mcp_server=True)
```
</div>

---
layout: center
---

# My 2 cents

- MCP is a promising approach to enhance AI applications by integrating external capabilities in a standardized way.
- [From the researcher perspective:]{style=background-color:lightblue;padding:3px;font-weight:900} LLMs can take away some of our manual labour and let us focus on the fun stuff (research, coming up with ideas, have agents explore )
- [From the developer perspective:]{style=background-color:lightblue;padding:3px;font-weight:900}  MCP can help to build more modular and maintainable AI applications, reducing the complexity of integrating multiple tools and resources.
- Community standard under open license

---
layout: center
---

# Use Cases

Use cases for scientific software and research data are just emerging: 
- Use natural language to query databases, run computations or populate LIMS 
- Help new users to get started with complex scientific software or to translate workflows 
- Solve tech debt in legacy scientific software

---
layout: center
---

# Learn more

- [HuggingFace Course on MCP](https://huggingface.co/learn/mcp-course)
- [Model Context Protocol (MCP) Documentation](https://modelcontextprotocol.io/docs/getting-started/intro)

# %% [markdown]
# # Generating New Music with Artificial Intelligence

# %% [markdown]
# ## Import Packages

# %%
import torchaudio
import audiocraft
from audiocraft.models import MusicGen
from IPython.display import Audio
from ipywidgets import Textarea  
from ipywidgets import Button

# %% [markdown]
# ## Load Pretrained Model

# %%
model = MusicGen.get_pretrained('facebook/musicgen-small')


# %% [markdown]
# ## Configure Model Parameters

# %%
model.set_generation_params(duration=8)


# %% [markdown]
# ## Generate Music

# %%
 results = model.generate(['classic rock song'])
 sampling_rate =  model.sample_rate
 Audio(results[0].numpy(), rate=sampling_rate)


# %% [markdown]
# ## Build a Text Input

# %%
description = Textarea(rows=4)
description


# %% [markdown]
# ## Generate Button

# %%
generate_button = Button(description="Generate Tune")
generate_button


# %% [markdown]
# ## Connect UI to the Model

# %%
# Create a text area and a button
description = Textarea(value='', placeholder='Give a music prompt', disabled=False, rows=4)
generate_button = Button(description="Generate Tune")


# A function to generate music as prompted
def generate_tune(event):
    results = model.generate([description.value])
    sampling_rate =  model.sample_rate
display( Audio(results[0].numpy(), rate=sampling_rate) )

# Create a click event on the button
generate_button.on_click(generate_tune)


# Display the UI items
display(description)
display(generate_button)


# %% [markdown]
# ## Refine Prompts

# %%
 results = model.generate(['upbeat rock song with guitar solo'])
 sampling_rate =  model.sample_rate
 Audio(results[0].numpy(), rate=sampling_rate)


# %%
 results = model.generate(['rock song'])
 sampling_rate =  model.sample_rate
 Audio(results[0].numpy(), rate=sampling_rate)

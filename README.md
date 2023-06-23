# 🤖 Unconditional MusicGen Trainer 🤖

This repository extends the [Audiocraft](https://github.com/facebookresearch/audiocraft) repository with a Trainer Class which trains the finetuned model unconditional.
Input prompts are the same for all the data trained on. The model converges but old learned sounds will vanish. 

* No input prompts
* Generating long sequences -> longer than 30 seconds 

## Installation

    
    !pip install 'torch>=2.0' 
    !pip install -U audiocraft 
    !pip install wandb #optional
    

## Training

    from train import main

    dataset_cfg = dict(
            dataset_path_train = "train",
            dataset_path_eval = "eval",
            batch_size=4,
            num_examples_train= 1000,
            num_examples_eval= 200,
            segment_duration= 30,
            sample_rate= 32_000,
            shuffle= True,
            return_info= False)

    cfg = dict(
        learning_rate = 0.0001,
        epochs = 80,
        model = "small",
        seed = (hash("blabliblu") % 2**32 - 1)
    )

    main("Model Name", cfg, dataset_cfg, 1, 'Wandb Project Name')


## Generation
The text prompt is replaced by audio (half of it) previously generated. Therefore, the model can generate new samples that are coherent. 

    from generate_inf import generate_long_seq
    from util import display_audio

    out = generate_long_seq(model, 8, 1024, True, 1.0, 250, 0, None)
    display_audio(out, path="audioSamples.wav")


## Citations

```
@article{copet2023simple,
      title={Simple and Controllable Music Generation},
      author={Jade Copet and Felix Kreuk and Itai Gat and Tal Remez and David Kant and Gabriel Synnaeve and Yossi Adi and Alexandre Défossez},
      year={2023},
      journal={arXiv preprint arXiv:2306.05284},
}
```

Thanks to Chavinlo who already made a [MusicGen Trainer](https://github.com/chavinlo/musicgen_trainer) that helped me develop my code.
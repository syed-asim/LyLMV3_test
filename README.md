# LyLMV3

This directory contains a script, `finetune_form_model.py`, that can be used to fine-tune (or evaluate) LayoutLMv3 on form understanding datasets, such as [FUNSD](https://guillaumejaume.github.io/FUNSD/) and [CORD](https://github.com/clovaai/cord).

The script `finetune_form_model.py` leverages the 🤗 Datasets library and the Trainer API. You can easily customize it to your needs.

## Fine-tuning on FUNSD

Fine-tuning LayoutLMv3 for token classification on [FUNSD](https://guillaumejaume.github.io/FUNSD/) can be done as follows:

```bash
python finetune_form_model.py \
  --model_name_or_path microsoft/layoutlmv3-base \
  --dataset_name funsd \
  --output_dir models \
  --do_train \
  --do_eval \
  --max_steps 1000 \
  --evaluation_strategy steps \
  --eval_steps 100 \
  --learning_rate 1e-5 \
  --load_best_model_at_end \
  --metric_for_best_model "eval_f1" \
  --push_to_hub \
  --push_to_hub°model_id layoutlmv3-finetuned-funsd
```

👀 The resulting model can be found here: https://huggingface.co/nielsr/layoutlmv3-finetuned-funsd. By specifying the `push_to_hub` flag, the model gets uploaded automatically to the hub (regularly), together with a model card, which includes metrics such as precision, recall and F1. Note that you can easily update the model card, as it's just a README file of the respective repo on the hub.

There's also the "Training metrics" [tab](https://huggingface.co/nielsr/layoutlmv3-finetuned-funsd/tensorboard), which shows Tensorboard logs over the course of training. Pretty neat, huh?

## Fine-tuning on CORD

Fine-tuning LayoutLMv3 for token classification on [CORD](https://github.com/clovaai/cord) can be done as follows:

```bash
python finetune_form_model.py \
  --model_name_or_path microsoft/layoutlmv3-base \
  --dataset_name cord \
  --output_dir layoutlmv3-test \
  --do_train \
  --do_eval \
  --max_steps 1000 \
  --evaluation_strategy steps \
  --eval_steps 100 \
  --learning_rate 5e-5 \
  --load_best_model_at_end \
  --metric_for_best_model "eval_f1" \
  --push_to_hub \
  --push_to_hub°model_id layoutlmv3-finetuned-cord
```

👀 The resulting model can be found here: https://huggingface.co/nielsr/layoutlmv3-finetuned-cord. Note that a model card gets generated automatically in case you specify the `push_to_hub` flag.
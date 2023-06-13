# DisneyGPT

* [Based on eniompw/nanoGPTshakespeare](https://github.com/eniompw/nanoGPTshakespeare)
* [Based on karpathy/nanoGPT](https://github.com/karpathy/nanoGPT)


### Train GPT
`!cd ./nanoGPT && python train.py --dataset=disney --dtype=float16 --eval_iters=20 --log_interval=1 --block_size=64 --batch_size=12 --n_layer=4 --n_head=4 --n_embd=128 --lr_decay_iters=2001 --dropout=0.0 --max_iters=2000 --eval_interval=500`

### Run GPT

`!cd ./nanoGPT && python sample.py --dtype=float16 --num_samples=5 --max_new_tokens=10 --start=" "`

### Notes
* `init_from = 'resume' # 'scratch' or 'resume' or 'gpt2*'`
* `lr_decay_iters=2000 --max_iters=2000 # causes ZeroDivisionError`

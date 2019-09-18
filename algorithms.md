YOLO
---

`Subdivisions`
-

It's how many mini batches you split your batch in.  
Batch=64 -> loading 64 images for this "iteration".  
Subdivision=8 -> Split batch into 8 "mini-batches" so 64/8 = 8 images per "minibatch" and this get sent to the gpu for process.  
That will be repeated 8 times until the batch is completed and a new itereation will start with 64 new images.

When batching you are averaging over more images the intend is not only to speed up the training process but also to generalise the training more.

If your GPU have enough memory you can reduce the subdivision to load more images into the gpu to process at the same time.

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTI0MjQ3NDU0NiwtMjAwNDQxMzgxNiw5NT
Q4NDcwMjVdfQ==
-->
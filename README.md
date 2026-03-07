## [Alibaba-NLP/gte-multilingual-base](https://huggingface.co/Alibaba-NLP/gte-multilingual-base)

|`max_position_embeddings`|`hidden_size`|`num_hidden_layers`|`pooling`
|-:|-:|-:|-:|
|`8192`|`768`|`12`|`cls`

```4d
var $en; $fr : 4D.Vector
var $AIClient : cs.AIKit.OpenAI
var $cosineSimilarity : Real
$AIClient:=cs.AIKit.OpenAI.new()

$AIClient.baseURL:="http://127.0.0.1:8080/v1"  

$batch:=$AIClient.embeddings.create(["query: Comment réinitialiser mon mot de passe?"; "passage: To reset your password you must contanct customer support."])

$fr:=$batch.embeddings[0].embedding
$en:=$batch.embeddings[1].embedding

$cosineSimilarity:=$fr.cosineSimilarity($en)

ALERT([$cosineSimilarity].join())
```

##### Cosine similarity from example code above:

|ONNX Runtime `Int8`|
|-|
|`0.72446597387183`|

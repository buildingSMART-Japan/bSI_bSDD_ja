# RDF

リソース記述フレームワーク（RDF）は、ウェブ上でのデータ交換のための標準モデルである。 続きを読む: https://www.w3.org/RDF/

bSDDにはRDF形式でデータを返す機能があるが、現在はPREVIEWの状態だ。

以下のAPIはRDFでデータを返すことをサポートしています：

- /api/分類/v3

キー "Accept"、値 "application/rdf+xml "のHTTPヘッダーを追加することで、RDF-xml形式の出力を要求できる。

application/x-turtle "のキー "Accept "と値 "text/turtle "を持つHTTPヘッダーを追加することで、タートル形式の出力を要求できる。

<img src="https://github.com/buildingSMART/bSDD/blob/documentation/Documentation/graphics/HowToGetOutputInTurtleFormat.PNG" alt="How to get output in turtle format"/>

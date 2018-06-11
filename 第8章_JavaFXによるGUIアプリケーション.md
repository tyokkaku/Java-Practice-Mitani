# 第8章　JavaFXによるGUIアプリケーション

## アプリケーションの作成

### GUIアプリケーションとJavaFXライブラリ

コントロール：JavaFXのアプリケーションでは、ウィンドウ上に配置されるボタンやテキスト入力ボックスなどの部品をコントロールと呼ぶ

### 初めてのアプリケーションの作成

javafx.application.Applicationクラスを継承する

```java
import javafx.application.Application;
import javafx.stage.Stage;

public class SimpleApplication extends Application {
    public void start(Stage stage) {  // startメソッドをオーバーライド、stageを渡す
        stage.setTitle("JavaFX Example");
        stage.setWidth(300);
        stage.setHeight(200);
        stage.show();
    }

    public static void main(String[] args) {
        launch();
    }
}
```

## コントロールの配置

- Stageオブジェクト
  - Sceneオブジェクト
    - Paneオブジェクト(ルートペイン)
      - StackPane、GridPane、BorderPaneなど
      - Controlss(ノード)

コントロールをのせたペインオブジェクトを、シーンを介して、ステージに配置する

GUIアプリケーションの部品をのせるオブジェクトを「コンテナ」と呼ぶこともある。(StageやPaneなど)

### コントロールを持つアプリケーションの基本

画面を設定し、部品を作り、部品を配置し、それらをまとめて、画面に表示する

```java
import javafx.application.Application;
import javafx.scene.Scene;
import javafx.scene.control.Button;
import javafx.scene.layout.FlowPane;
import javafx.stage.Stage;

public class LayoutExample extends Application {

    public void start(Stage stage) {
        // (1) メインウィンドウ(Stage)の設定
        stage.setWidth(280);
        stage.setHeight(100);

        // (2) コントロールの生成
        Button button1 = new Button("January");
        Button button2 = new Button("February");
        Button button3 = new Button("March");
        Button button4 = new Button("April");

        // (3) ルートペインを生成し、コントロールを配置
        FlowPane root = new FlowPane();
        root.getChildren().add(button1);
        root.getChildren().add(button2);
        root.getChildren().add(button3);
        root.getChildren().add(button4);
        button1.setPrefSize(80, 30);
        button2.setPrefSize(80, 30);
        button3.setPrefSize(80, 30);
        button4.setPrefSize(80, 30);

        // (4) ルートペインをもとにシーンを生成
        Scene scene = new Scene(root);

        // (5) ステージにシーンを配置
        stage.setScene(scene);

        // (6) アプリケーションウィンドウを表示
        stage.show();
    }
    public static void main(String[] args) {
        launch();
    }
}
```

### コントロールのサイズ指定

- setPrefSize
- setPrefWidth
- setPrefHeight
- setMaxSize
- setMinSize

### さまざまなペインクラスとコントロールの配置

ペインの種類によって、コントロールの配置のされ方が異なる。以下のペインは、いずれもjavafx.scene.layoutパッケージに含まれる。

### ボーダーペイン

FlowPaneとあまり違わない

```java
// (3) ルートペインを生成し、コントロールを配置
BorderPane root = new BorderPane();
root.setTop(button1);
root.setLeft(button2);
root.setCenter(button3);
root.setRight(button4);
root.setBottom(button5);
```

### グリッドペイン

格子状に配置する。addAllを使用すれば、複数のコントロールをまとめて配置できる。

```java
// (2) コントロールの生成
Button button1 = new Button("(0, 0)");
Button button2 = new Button("(1, 1)");
Button button3 = new Button("(2, 2)");
Button button4 = new Button("(0, 2)");

button1.setPrefSize(80, 30);
button2.setPrefSize(80, 30);
button3.setPrefSize(80, 30);
button4.setPrefSize(80, 30);

// (3) ルートペインを生成し、コントロールを配置
GridPane root = new GridPane();
GridPane.setConstraints(button1, 0, 0);
GridPane.setConstraints(button2, 1, 1);
GridPane.setConstraints(button3, 2, 2);
GridPane.setConstraints(button4, 0, 2);
root.getChildren().addAll(button1, button2, button3, button4);
```

### ボックスペイン

HBox：縦
VBox：横

```java
// (2) コントロールの生成
Button button1 = new Button("A");
Button button2 = new Button("B");
Button button3 = new Button("C");
Button button4 = new Button("D");
button1.setPrefSize(50, 20);
button2.setPrefSize(50, 20);
button3.setPrefSize(50, 20);
button4.setPrefSize(50, 20);

// (3) ルートペインを生成し、コントロールを配置
VBox root = new VBox(10);
root.getChildren().addAll(button1, button2, button3, button4);
```

### 複数のペインの組み合わせ

rootPaneにButton3つとsubPaneを配置する。subPaneにはボタン4つが配置されている。

```java
        // (2) コントロールの生成
        Button button1 = new Button("1");
        Button button2 = new Button("2");
        Button button3 = new Button("3");
        Button button4 = new Button("4");
        Button button5 = new Button("5");
        Button button6 = new Button("6");
        Button button7 = new Button("7");

        button1.setPrefSize(200, 100);
        button2.setPrefSize(200, 100);
        button3.setPrefSize(200, 100);
        button4.setPrefSize(100, 50);
        button5.setPrefSize(100, 50);
        button6.setPrefSize(100, 50);
        button7.setPrefSize(100, 50);

        GridPane subPane = new GridPane();
        GridPane.setConstraints(button4, 0, 0);
        GridPane.setConstraints(button5, 1, 0);
        GridPane.setConstraints(button6, 0, 1);
        GridPane.setConstraints(button7, 1, 1);

        subPane.getChildren().addAll(button4, button5, button6, button7);

        // (3) ルートペインを生成し、コントロールを配置
        GridPane root = new GridPane();
        GridPane.setConstraints(button1, 0, 0);
        GridPane.setConstraints(button2, 1, 0);
        GridPane.setConstraints(button3, 0, 1);
        GridPane.setConstraints(subPane, 1, 1);

        root.getChildren().addAll(button1, button2, button3, subPane);
```

- コントロール：部品
- ペイン：部品をのせるもの。配置の方法には色々ある
- ルートペイン：ペインやコントロールの階層構造における起点
- ノード：ペインやコントロールを階層構造で表したときに、それぞれの階層にあたるペインやコントロールの総称
- シーン：ウィンドウ内の表示領域に対応するオブジェクト。ルートペインをシーンにのせ、シーンをステージにのせる。
- ステージ：アプリケーションのウィンドウに相当するオブジェクト

## イベント処理

イベントハンドラ：イベントの通知を受け取ってイベント処理を行うオブジェクトのこと。実際に働くもの。イベントが発生したときの通知先を登録することを、イベントハンドラを登録する、という。

buttonオブジェクトを生成。ButtonクラスのsetOnActionメソッドで、イベントハンドラを登録。setOnActionの引数は、EventHandler<ActionEvent>インタフェースで、このインタフェースのhandleメソッドをオーバライドすることでイベント処理の内容を記述している。

```java
Button button = new Button("ボタン");
button.setOnAction(new EventHandler<ActionEvent>()) {
  public void handle(ActionEvent event) {
    System.out.println("ボタンが押されました");
  }
});
```

EventHandler<ActionEvent>は関数型インタフェースであり、ラムダ式を用いて短く記述できる。

```java
Button button = new Button("ボタン");
button.setOnaCtion(event -> System.out.println("ボタンが押されました"));
```

### イベント処理の例

ボタンが表示されました、と標準出力するイベント処理

```java
import javafx.application.Application;
import javafx.scene.Scene;
import javafx.scene.control.Button;
import javafx.scene.layout.BorderPane;
import javafx.stage.Stage;

public class EventHandle extends Application {
    public void start(Stage stage) {
        // メインウィンドウ設定
        stage.setWidth(300);
        stage.setHeight(140);

        // コントロール生成
        Button button = new Button("ボタン");
        button.setOnAction(event -> System.out.println("ボタンが押されました"));

        // ルートペインに配置
        BorderPane root = new BorderPane();
        root.setCenter(button);

        // シーン生成
        stage.setScene(new Scene(root));

        // ステージに乗っける
        stage.show();
    }

    public static void main(String[] args) {
        launch();
    }
}
```

### さまざまなコントロールを持つアプリケーションの例

```java
import javafx.application.Application;
import javafx.geometry.Insets;
import javafx.scene.Scene;
import javafx.scene.control.*;
import javafx.scene.layout.*;
import javafx.stage.Stage;

public class Controls extends Application {
  CheckBox checkBox; // チェックボックス
	ChoiceBox<String> choiceBox; // チョイスボックス
	Slider slider; // スライダー
	Label label; // ラベル
	TextField textField; // テキストフィールド
	RadioButton radioButton1; // ラジオボタン1
	RadioButton radioButton2; // ラジオボタン2
	RadioButton radioButton3; // ラジオボタン3
	ToggleGroup toggleGroup;
	Button button; // ボタン
	TextArea textArea; // テキストエリア

	public void start(Stage stage) {
		stage.setWidth(500);
		stage.setHeight(350);

		checkBox = new CheckBox("チェックボックス");

		choiceBox = new ChoiceBox<>();
		choiceBox.getItems().addAll("チョイスボックス1", "チョイスボックス2", "チョイスボックス3");
		choiceBox.setValue("チョイスボックス1");

		radioButton1 = new RadioButton("ラジオボタン1");
		radioButton2 = new RadioButton("ラジオボタン2");
		radioButton3 = new RadioButton("ラジオボタン3");
		toggleGroup = new ToggleGroup();
		radioButton1.setToggleGroup(toggleGroup);
		radioButton2.setToggleGroup(toggleGroup);
		radioButton3.setToggleGroup(toggleGroup);
		radioButton1.setSelected(true);

		label = new Label("ラベル");

		slider = new Slider(0, 100, 50);
		slider.setShowTickMarks(true);
		slider.setShowTickLabels(true);
		slider.setOnMouseClicked(event -> label.setText("スライダーの値：" + (int) slider.getValue()));

		textField = new TextField("テキストフィールド");

		button = new Button("OK");
		button.setOnAction(event -> buttonPressed());

		textArea = new TextArea("テキストエリア");

		VBox box = new VBox(5);
		box.setPadding(new Insets(20, 25, 25, 25));

		box.getChildren().addAll(checkBox, radioButton1, radioButton2, radioButton3, choiceBox, slider, label,
				textField, button);

		MenuBar menuBar = new MenuBar();
		Menu fileMenu = new Menu("ファイル");
		MenuItem menuOpen = new MenuItem("開く");
		MenuItem menuExit = new MenuItem("終了");
		menuExit.setOnAction(event -> System.exit(0));
		fileMenu.getItems().add(menuOpen);
		fileMenu.getItems().add(menuExit);
		menuBar.getMenus().add(fileMenu);

		BorderPane root = new BorderPane();
		root.setLeft(box);
		root.setTop(menuBar);
		root.setCenter(textArea);

		stage.setScene(new Scene(root));
		stage.show();
	}

	void buttonPressed() {
		textArea.clear();
		textArea.appendText("チェックボックスの選択状態:" + checkBox.isSelected());
		textArea.appendText("\nラジオボタンの選択項目:" + ((RadioButton) toggleGroup.getSelectedToggle()).getText());
		textArea.appendText("\nチョイスボックスの選択項目:" + choiceBox.getValue());
		textArea.appendText("\nスライダーの値:" + slider.getValue());
		textArea.appendText("\nテキストフィールドの文字列:" + textField.getText());
	}

	public static void main(String[] args) {
		launch();
	}
}

```

練習問題

8.1
1:g
2:e
3:f
4:c
5:b
6:h
7:i
8:a

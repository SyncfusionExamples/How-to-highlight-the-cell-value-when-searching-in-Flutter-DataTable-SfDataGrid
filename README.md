# How to highlight the cell value when searching in Flutter DataTable (SfDataGrid)?

In this article, we will show you how to highlight the cell value when searching in [Flutter DataTable](https://www.syncfusion.com/flutter-widgets/flutter-datagrid).

Initialize the [SfDataGrid](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/SfDataGrid-class.html) widget with all the necessary properties.  Within the [DataGridSource.buildRow()](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/DataGridSource/buildRow.html), if [searchController.text](https://api.flutter.dev/flutter/widgets/TextEditingController/text.html) is equal to the corresponding cell value, you should add the appropriate style to highlight the text in the cell. Additionally, remember to call [notifyListeners](https://api.flutter.dev/flutter/foundation/ChangeNotifier/notifyListeners.html) when the searchController.text changes, to refresh the DataGrid and apply highlighting to the searched cell value.

```dart
Widget searchField() {
    return Container(
      width: 200,
      height: 50,
      decoration: BoxDecoration(
        border: Border.all(
          color: Colors.grey,
          width: 1.0,
        ),
        borderRadius: BorderRadius.circular(8.0),
      ),
      child: TextField(
        controller: employeeDataSource.searchController,
        onChanged: (v) {
          employeeDataSource.refreshDataGridSource();
          initiateScrolling();
        },
        decoration: const InputDecoration(
          hintText: "Search",
        ),
      ),
    );
  }


class EmployeeDataSource extends DataGridSource {
  …

  @override
  DataGridRowAdapter buildRow(DataGridRow row) {
    return DataGridRowAdapter(
      cells: row.getCells().map<Widget>((e) {
        TextStyle? getTextStyle() {
          if (searchController.text.toLowerCase() ==
              e.value.toString().toLowerCase()) {
            return TextStyle(
                fontWeight: FontWeight.bold,
                color: Colors.pinkAccent,
                background: Paint()..color = Colors.yellow);
          } else {
            return null;
          }
        }

        return Container(
          alignment: Alignment.center,
          padding: const EdgeInsets.all(8.0),
          child: Text(
            e.value.toString(),
            style: getTextStyle(),
          ),
        );
      }).toList(),
    );
  }
```

You can download the example from [GitHub](https://github.com/SyncfusionExamples/How-to-highlight-the-cell-value-when-searching-in-Flutter-DataTable-SfDataGrid).
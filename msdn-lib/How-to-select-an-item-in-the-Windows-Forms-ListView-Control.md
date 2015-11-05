
[Source](https://msdn.microsoft.com/en-us/library/y4x56c0b(v=vs.110).aspx "Permalink to Select an Item in the Windows Forms ListView Control")

# Select an Item in the Windows Forms ListView Control


This example demonstrates how to programmatically change the selection in a Windows Forms [ListView][2] control. Selecting an item programmatically does not automatically change the focus to the [ListView][2] control. For this reason, you will typically also want to set the item as focused when selecting an item.

```vbnet
    'It is highly recommended that Visual Basic code files enable Option Strict as it prevents many simple, common mistakes.
    Option Strict On

    Public Class Form1
        'These lines of code create the user controls for the example.
        'Typically this code will be generated for you when you drag the controls on the form in the designer.
        'For ease of using the sample, you can paste this code over the default Form1 code of new Windows Forms Application project.

        'Create a TableLayoutPanel to easily arrange the user controls on the Form.
        Friend WithEvents TableLayoutPanel1 As New TableLayoutPanel With {.Dock = DockStyle.Fill}
        'Create the ListView
        Friend WithEvents ListView1 As New ListView With {.Anchor = AnchorStyles.Top Or AnchorStyles.Bottom Or AnchorStyles.Left Or AnchorStyles.Right, .HideSelection = False}
        'Create a Button to select the next item in the ListView
        Friend WithEvents SelectNextButton As New Button With {.AutoSize = True, .Text = "Select Next"}

        Private Sub Form1_Load(sender As Object, e As EventArgs) Handles MyBase.Load
            'call the helper method to configure the user interface
            ConfigureExampleForm()
            'call the helper method to add example items to the ListView
            LoadExampleItems()
        End Sub

        'Here we'll handle the Click event on the SelectNextButton to move the current selection
        'in the ListView to the next item.  If the last item in the ListView is selected we will
        'move back to the first item.
        Private Sub SelectNextButton_Click(sender As Object, e As EventArgs) Handles SelectNextButton.Click
            'The ListView can be configured to allow various item selection behavior.  By default the
            'ListView will allow multiple selections so we will discover the index of the last selected item.
            'We will then move the selection to the next higher index, or return to the first index if we 
            'are already at the last item.

            'We will use -1 to indicate that no item is currently selected in the ListView.  This is a value
            'commonly used when a list control does not have an item currently selected.
            Dim lastSelectedIndex As Integer = -1
            'By checking the count of items in the ListView we can determine if there is a selected item, and if so,
            'the index of the last selected item.
            If ListView1.SelectedIndices.Count > 0 Then
                lastSelectedIndex = ListView1.SelectedIndices(ListView1.SelectedIndices.Count - 1)
            End If
            'Now that we have determined the currently selected index we can increase the value by 1.
            lastSelectedIndex += 1
            'Finally, we need to ensure that the new index value is within the range of items in the ListView.
            If lastSelectedIndex = ListView1.Items.Count Then
                'If the new index equals the number of items in the list then we need to return to the first
                'index (which is always zero).
                lastSelectedIndex = 0
            End If

            'Now that we have a new valid index, we can set the selection in the ListView by accessing the item
            'at the new index and setting it's Selected property value to True.  Before we do however, we may wish
            'to clear the current selection.  Without this line of code we will cause the ListView to select multiple items.
            ListView1.SelectedIndices.Clear()
            ListView1.Items(lastSelectedIndex).Selected = True
            'Changing the selected item in code does not automatically shift focus to that item so you may also
            'wish to set focused state of the item.
            ListView1.Items(lastSelectedIndex).Focused = True
        End Sub

        'Configure the example Form by adding the FlowLayoutPanel to the Form,
        'and then adding the user controls to the FlowLayoutPanel.
        Private Sub ConfigureExampleForm()
            Controls.Add(TableLayoutPanel1)
            TableLayoutPanel1.RowCount = 2
            TableLayoutPanel1.ColumnCount = 2

            TableLayoutPanel1.Controls.Add(SelectNextButton, 0, 0)
            TableLayoutPanel1.Controls.Add(ListView1, 0, 1)
            TableLayoutPanel1.SetColumnSpan(ListView1, 2)
        End Sub

        'Load 10 example items into the ListView.
        Private Sub LoadExampleItems()
            For i As Integer = 1 To 10
                ListView1.Items.Add("Item " & i.ToString)
            Next
        End Sub
    End Class
```
```csharp
    using System;
    using System.Collections.Generic;
    using System.ComponentModel;
    using System.Data;
    using System.Drawing;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Windows.Forms;

    namespace WindowsFormsApplication1
    {
        public partial class Form1 : Form
        {
            //These lines of code create the user controls for the example.
            //Typically this code will be generated for you when you drag the controls on the form in the designer.
            //For ease of using the sample, you can paste this code over the default Form1 code of new Windows Forms Application project.

            //Create a TableLayoutPanel to easily arrange the user controls on the Form.
            private TableLayoutPanel TableLayoutPanel1 = new TableLayoutPanel { Dock = DockStyle.Fill };
            //Create the ListView
            private ListView ListView1 = new ListView { Anchor = AnchorStyles.Top | AnchorStyles.Bottom | AnchorStyles.Left | AnchorStyles.Right, HideSelection = false };
            //Create a Button to select the next item in the ListView
            private Button SelectNextButton = new Button { AutoSize = true, Text = "Select Next" };

            public Form1()
            {
                InitializeComponent();
            }

            private void Form1_Load(object sender, EventArgs e)
            {
                //call the helper method to configure the user interface
                ConfigureExampleForm();
                //call the helper method to add example items to the ListView
                LoadExampleItems();
            }

            //Here we'll handle the Click event on the SelectNextButton to move the current selection
            //in the ListView to the next item.  If the last item in the ListView is selected we will
            //move back to the first item.
            private void SelectNextButton_Click(Object sender, EventArgs e)
            {
                //The ListView can be configured to allow various item selection behavior.  By default the
                //ListView will allow multiple selections so we will discover the index of the last selected item.
                //We will then move the selection to the next higher index, or return to the first index if we 
                //are already at the last item.

                //We will use -1 to indicate that no item is currently selected in the ListView.  This is a value
                //commonly used when a list control does not have an item currently selected.
                int lastSelectedIndex = -1;
                //By checking the count of items in the ListView we can determine if there is a selected item, and if so,
                //the index of the last selected item.
                if (ListView1.SelectedIndices.Count > 0)
                    lastSelectedIndex = ListView1.SelectedIndices[ListView1.SelectedIndices.Count - 1];

                //Now that we have determined the currently selected index we can increase the value by 1.
                lastSelectedIndex += 1;
                //Finally, we need to ensure that the new index value is within the range of items in the ListView.
                if (lastSelectedIndex == ListView1.Items.Count)
                    //If the new index equals the number of items in the list then we need to return to the first
                    //index (which is always zero).
                    lastSelectedIndex = 0;

                //Now that we have a new valid index, we can set the selection in the ListView by accessing the item
                //at the new index and setting it//s Selected property value to True.  Before we do however, we may wish
                //to clear the current selection.  Without this line of code we will cause the ListView to select multiple items.
                ListView1.SelectedIndices.Clear();
                ListView1.Items[lastSelectedIndex].Selected = true;
                //Changing the selected item in code does not automatically shift focus to that item so you may also
                //wish to set focused state of the item.
                ListView1.Items[lastSelectedIndex].Focused = true;
            }

            //Configure the example Form by adding the FlowLayoutPanel to the Form,
            //and then adding the user controls to the FlowLayoutPanel.
            private void ConfigureExampleForm()
            {
                Controls.Add(TableLayoutPanel1);
                TableLayoutPanel1.RowCount = 2;
                TableLayoutPanel1.ColumnCount = 2;

                TableLayoutPanel1.Controls.Add(SelectNextButton, 0, 0);
                TableLayoutPanel1.Controls.Add(ListView1, 0, 1);
                TableLayoutPanel1.SetColumnSpan(ListView1, 2);

                SelectNextButton.Click += SelectNextButton_Click;
            }

            //Load 10 example items into the ListView.
            private void LoadExampleItems()
            {
                for (int i = 1; i < 11; i++)
                {
                    ListView1.Items.Add("Item " + i.ToString());
                }
            }
        }
    }
```

##Compiling the Code
To use the sample, create a new Windows Forms application and paste the following code over the default Form1 code.

##See Also
[ListView][2]

[ListViewItem.Selected][5]

[1]: https://i-msdn.sec.s-msft.com/Areas/Epx/Content/Images/ImageSprite.png?v=635810750817785875
[2]: https://msdn.microsoft.com/en-us/library/system.windows.forms.listview(v=vs.110).aspx  
[3]: https://msdn.microsoft.com/en-us/library/system(v=vs.110).aspx
[4]: https://msdn.microsoft.com/en-us/library/system.windows.forms(v=vs.110).aspx
[5]: https://msdn.microsoft.com/en-us/library/system.windows.forms.listviewitem.selected(v=vs.110).aspx

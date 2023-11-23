# filtro-de-precio
reusar solo el codigo que hay aqui:
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Reducir descripcion</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/PapaParse/5.3.0/papaparse.min.js"></script>
</head>
<body>
    <input type="file" id="csvFileInput" accept=".csv">
    <button onclick="handleCSV()">Convertir CSV a Modelo</button>

    
    <script>
        class ProductModel {
            constructor(data) {
                this.HandleId = data.HandleId || '';
                this.FieldType = data.FieldType || 'Product';
                this.Name = data.Name || '';
                this.Description = data.Description || '';
                this.ProductImageUrl = data.ProductImageUrl || '';
                this.Collection = data.Collection || '';
                this.SKU = data.SKU || '';
                this.Ribbon = data.Ribbon || '';
                this.Price = parseFloat(data.Price) || 0;
                this.Surcharge = parseFloat(data.Surcharge) || 0;
                this.Visible = true;
                if (this.Price === 0) {
                        this.Visible = false;
                    } else {
                        this.Visible = data.Visible === true;
                    }
                this.DiscountMode = data.DiscountMode || 'PERCENT';
                this.DiscountValue = parseFloat(data.DiscountValue) || 0;
                this.Inventory = parseInt(data.Inventory) || 0;
                if (this.Inventory < 10) {
                     this.Inventory = 'OUT_OF_STOCK';
                    }
                this.Weight = parseFloat(data.Weight) || 0;
                this.Cost = parseFloat(data.Cost) || 0;
                this.ProductOptionName1 = data.ProductOptionName1 || '';
                this.ProductOptionType1 = data.ProductOptionType1 || '';
                this.ProductOptionDescription1 = data.ProductOptionDescription1 || '';
                this.ProductOptionName2 = data.ProductOptionName2 || '';
                this.ProductOptionType2 = data.ProductOptionType2 || '';
                this.ProductOptionDescription2 = data.ProductOptionDescription2 || '';
                this.ProductOptionName3 = data.ProductOptionName3 || '';
                this.ProductOptionType3 = data.ProductOptionType3 || '';
                this.ProductOptionDescription3 = data.ProductOptionDescription3 || '';
                this.ProductOptionName4 = data.ProductOptionName4 || '';
                this.ProductOptionType4 = data.ProductOptionType4 || '';
                this.ProductOptionDescription4 = data.ProductOptionDescription4 || '';
                this.ProductOptionName5 = data.ProductOptionName5 || '';
                this.ProductOptionType5 = data.ProductOptionType5 || '';
                this.ProductOptionDescription5 = data.ProductOptionDescription5 || '';
                this.ProductOptionName6 = data.ProductOptionName6 || '';
                this.ProductOptionType6 = data.ProductOptionType6 || '';
                this.ProductOptionDescription6 = data.ProductOptionDescription6 || '';
                // ... (repite para otras opciones)
                this.AdditionalInfoTitle1 = data.AdditionalInfoTitle1 || '';
                this.AditionalInfoDescription2 = data.AditionalInfoDescription2 || '';
                this.AdditionalInfoTitle3 = data.AdditionalInfoTitle3 || '';
                this.AditionalInfoDescription3 = data.AditionalInfoDescription3 || '';
                this.AdditionalInfoTitle4 = data.AdditionalInfoTitle4 || '';
                this.AditionalInfoDescription4 = data.AditionalInfoDescription4 || '';
                this.AdditionalInfoTitle5 = data.AdditionalInfoTitle5 || '';
                this.AditionalInfoDescription5 = data.AditionalInfoDescription5 || '';
                this.AdditionalInfoTitle6 = data.AdditionalInfoTitle6 || '';
                this.AditionalInfoDescription6 = data.AditionalInfoDescription6 || '';
                
                // ... (repite para otras informaciones adicionales)
                //this.CustomTextField1 =' ';
                //this.CustomTextCharLimit1 = 1;
                //this.CustomTextMandatory1 = false;
                //this.CustomTextField2 =' ';
                //this.CustomTextCharLimit2 = 1;
                //this.CustomTextMandatory2 = false;
                this.Brand = data.Brand || '';
            }
        }

        function handleCSV() {

            const fileInput = document.getElementById('csvFileInput');
            const file = fileInput.files[0];

            if (file) {
                Papa.parse(file, {
                    header: true,
                    dynamicTyping: true,
                    complete: function (result) {
                        const dataArray = result.data.map(row => new ProductModel(row)).filter(product => product.Price >= 12);
                        // Haz lo que quieras con el arreglo de objetos
                        console.log(dataArray);
                        const csvString = Papa.unparse(dataArray, {
                            header: true,
                        });

                        const blob = new Blob([csvString], { type: 'text/csv' });
                        const url = URL.createObjectURL(blob);

                        const a = document.createElement('a');
                        a.href = url;
                        a.download = 'converted_data_Remaster.csv';
                        document.body.appendChild(a);
                        a.click();
                        document.body.removeChild(a);

                        // Liberar el objeto URL
                        URL.revokeObjectURL(url);
                    },
                    error: function (error) {
                        console.error('Error parsing CSV:', error.message);
                    }
                });
            } else {
                alert('Por favor, selecciona un archivo CSV.');
            }
        }
       
       function PriceFilter(){
        const fileInput = document.getElementById('csvFileInput_price');
            const file = fileInput.files[0];

            if (file) {
                Papa.parse(file, {
                    header: true,
                    dynamicTyping: true,
                    complete: function (result) {
                        const dataArray = result.data.map(row => new ProductModel(row));
                        // Haz lo que quieras con el arreglo de objetos
                        console.log(dataArray);
                        const csvString = Papa.unparse(dataArray, {
                            header: true,
                        });

                        const blob = new Blob([csvString], { type: 'text/csv' });
                        const url = URL.createObjectURL(blob);

                        const a = document.createElement('a');
                        a.href = url;
                        a.download = 'converted_data.csv';
                        document.body.appendChild(a);
                        a.click();
                        document.body.removeChild(a);

                        // Liberar el objeto URL
                        URL.revokeObjectURL(url);
                    },
                    error: function (error) {
                        console.error('Error parsing CSV:', error.message);
                    }
                });
            } else {
                alert('Por favor, selecciona un archivo CSV.');
            }
       }
        function cleanHTML(htmlString) {
            // Crear un objeto DOMParser
            var parser = new DOMParser();

            // Parsear la cadena HTML
            var doc = parser.parseFromString(htmlString, "text/html");

            // Obtener el texto sin etiquetas HTML
            return doc.body.textContent || "";
        }
    </script>
</body>
</html>


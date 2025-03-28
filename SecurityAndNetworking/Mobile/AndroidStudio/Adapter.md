`Adapter` objesi `AdapterView` ile view için gerekli veri arasında bir köprü görevi görür.  Adapter verilere erişimi sağlar . The Adapter is also responsible for making a View for each item in the data set.

Yani her bir veri için bir view oluşturmana yardımcı olur. 

Frontende kayıyıor yine

```kotlin
dependencies{  
  implementation 'androidx.recyclerview:recyclerview:1.3.2'    
  implementation 'androidx.cardview:cardview:1.0.0'  
}
```


```kotlin
import android.view.LayoutInflater  
import android.view.View  
import android.view.ViewGroup  
import android.widget.ImageView  
import android.widget.TextView  
import androidx.recyclerview.widget.RecyclerView  
  
class ProductAdapter(private val productList: List<Product>) : RecyclerView.Adapter<ProductAdapter.ProductViewHolder>() {  
  
    class ProductViewHolder(view: View) : RecyclerView.ViewHolder(view) {  
        val imageView: ImageView = view.findViewById(R.id.product_image)  
        val titleView: TextView = view.findViewById(R.id.product_title)  
        val descriptionView: TextView = view.findViewById(R.id.product_description)  
        val priceView: TextView = view.findViewById(R.id.product_price)  
    }  
  
    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): ProductViewHolder {  
        val view = LayoutInflater.from(parent.context).inflate(R.layout.item_product, parent, false)  
        return ProductViewHolder(view)  
    }  
  
    override fun onBindViewHolder(holder: ProductViewHolder, position: Int) {  
        val product = productList[position]  
        holder.imageView.setImageResource(product.imageResId)  
        holder.titleView.text = product.title  
        holder.descriptionView.text = product.description  
        holder.priceView.text = "${product.price}"  
        }  
  
    override fun getItemCount() = productList.size  
}
```
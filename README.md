package com.example.tokoparfum

import android.os.Bundle
import android.widget.Button
import android.widget.Toast
import androidx.appcompat.app.AppCompatActivity

class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val tombolBeli = findViewById<Button>(R.id.btnBeli)

        tombolBeli.setOnClickListener {
            Toast.makeText(this, "Parfum berhasil dibeli!", Toast.LENGTH_SHORT).show()
        }
    }
}<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical"
    android:padding="20dp"
    android:gravity="center"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <TextView
        android:text="Parfum Dior Sauvage"
        android:textSize="24sp"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"/>

    <TextView
        android:text="Harga: Rp 1.200.000"
        android:textSize="18sp"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"/>

    <Button
        android:id="@+id/btnBeli"
        android:text="Beli"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"/>

</LinearLayout>package com.example.tokoparfum

data class Perfume(
    val id: Int,
    val name: String,
    val price: Int,        // dalam rupiah
    val imageRes: Int      // referensi drawable
)package com.example.tokoparfum

import com.example.tokoparfum.R

val samplePerfumes = listOf(
    Perfume(1, "Parfum A", 350000, R.drawable.perfume_a),
    Perfume(2, "Parfum B", 450000, R.drawable.perfume_b),
    Perfume(3, "Parfum C", 550000, R.drawable.perfume_c)
)package com.example.tokoparfum

import android.os.Bundle
import android.widget.Toast
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.compose.foundation.Image
import androidx.compose.foundation.layout.*
import androidx.compose.foundation.lazy.LazyColumn
import androidx.compose.foundation.lazy.items
import androidx.compose.material3.Button
import androidx.compose.material3.Card
import androidx.compose.material3.MaterialTheme
import androidx.compose.material3.Text
import androidx.compose.runtime.Composable
import androidx.compose.ui.Modifier
import androidx.compose.ui.layout.ContentScale
import androidx.compose.ui.platform.LocalContext
import androidx.compose.ui.res.painterResource
import androidx.compose.ui.unit.dp
import com.example.tokoparfum.ui.theme.TokoParfumTheme

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            TokoParfumTheme {
                PerfumeListScreen(perfumes = samplePerfumes)
            }
        }
    }
}

@Composable
fun PerfumeListScreen(perfumes: List<Perfume>) {
    val context = LocalContext.current

    LazyColumn(
        modifier = Modifier
            .fillMaxSize()
            .padding(8.dp),
        verticalArrangement = Arrangement.spacedBy(8.dp)
    ) {
        items(perfumes) { perfume ->
            PerfumeItem(perfume) {
                // aksi beli
                Toast.makeText(
                    context,
                    "${perfume.name} berhasil dibeli!",
                    Toast.LENGTH_SHORT
                ).show()
            }
        }
    }
}

@Composable
fun PerfumeItem(perfume: Perfume, onBuyClicked: () -> Unit) {
    Card(
        modifier = Modifier
            .fillMaxWidth()
            .wrapContentHeight(),
        elevation = CardDefaults.cardElevation(defaultElevation = 4.dp)
    ) {
        Row(modifier = Modifier.padding(8.dp)) {
            Image(
                painter = painterResource(id = perfume.imageRes),
                contentDescription = perfume.name,
                modifier = Modifier
                    .size(80.dp)
                    .padding(end = 8.dp),
                contentScale = ContentScale.Crop
            )

            Column(
                modifier = Modifier
                    .weight(1f)
                    .padding(end = 8.dp)
            ) {
                Text(text = perfume.name, style = MaterialTheme.typography.titleMedium)
                Spac
    }
}
